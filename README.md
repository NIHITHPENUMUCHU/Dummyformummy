This is a very common and frustrating bug to run into, but the root cause is actually quite simple. Your backend is suffering from **"Server Amnesia."**

### Why is this happening?
Look at this exact line in your `JwtUtil.java` file:
`private final Key secretKey = Keys.secretKeyFor(SignatureAlgorithm.HS256);`

This line tells Spring Boot to generate a **brand new, randomized secret key** in memory every single time the server starts up. 

If you log in, the server gives you a token signed with **Key A**. Your Angular frontend saves that token. If you then restart your Spring Boot server (or if it auto-restarts), the server generates a new **Key B**. When your frontend tries to create an event using the token signed with Key A, the server checks it against Key B, says "JWT signature does not match," and throws the 403 error.

### The Fix
To fix this, we need to force the server to use a persistent, hardcoded secret string instead of generating a random one on startup. 

**Step 1: Add a persistent secret to your properties file.**
Open your `application.properties` and add a `jwt.secret` variable at the bottom. (JJWT HS256 requires the string to be at least 32 characters long).

```properties
# MySQL connection properties
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.username=root
spring.datasource.password=root
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

# Hibernate properties
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL5Dialect
spring.jpa.hibernate.ddl-auto=update

server.port=3000

# NEW: Persistent JWT Secret Key
jwt.secret=EventMasterProSuperSecretKeyThatIsVeryLongAndSecure12345!
```

**Step 2: Update `JwtUtil.java` to use the persistent secret.**
We will inject that property into your utility class and convert it into the `Key` object JJWT needs. Replace your entire `JwtUtil.java` with this:

```java
package com.edutech.eventmanagementsystem.jwt;

import io.jsonwebtoken.Claims;
import io.jsonwebtoken.Jwts;
import io.jsonwebtoken.security.Keys;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.stereotype.Service;

import java.security.Key;
import java.util.Date;
import java.util.HashMap;
import java.util.Map;
import java.util.function.Function;

@Service
public class JwtUtil {

    // THE FIX: Pulls the persistent secret from application.properties
    @Value("${jwt.secret}")
    private String secretString;

    // Helper method to convert the string into a secure Key object
    private Key getSigningKey() {
        return Keys.hmacShaKeyFor(secretString.getBytes());
    }

    public String extractUsername(String token) {
        return extractClaim(token, Claims::getSubject);
    }

    public Date extractExpiration(String token) {
        return extractClaim(token, Claims::getExpiration);
    }

    public <T> T extractClaim(String token, Function<Claims, T> claimsResolver) {
        final Claims claims = extractAllClaims(token);
        return claimsResolver.apply(claims);
    }

    private Claims extractAllClaims(String token) {
        return Jwts.parserBuilder()
                .setSigningKey(getSigningKey()) // Uses persistent key
                .build()
                .parseClaimsJws(token)
                .getBody();
    }

    private Boolean isTokenExpired(String token) {
        return extractExpiration(token).before(new Date());
    }

    public String generateToken(String username) {
        Map<String, Object> claims = new HashMap<>();
        return createToken(claims, username);
    }

    private String createToken(Map<String, Object> claims, String subject) {
        return Jwts.builder()
                .setClaims(claims)
                .setSubject(subject)
                .setIssuedAt(new Date(System.currentTimeMillis()))
                .setExpiration(new Date(System.currentTimeMillis() + 1000 * 60 * 60 * 10))
                .signWith(getSigningKey()) // Uses persistent key
                .compact();
    }

    public Boolean validateToken(String token, UserDetails userDetails) {
        final String username = extractUsername(token);
        return (username.equals(userDetails.getUsername()) && !isTokenExpired(token));
    }
}
```

**Step 3: Clear your browser and restart.**
Because your Angular frontend is currently holding onto an old token that will fail, you must **log out on the frontend (or clear your browser's Local Storage)** to wipe it. Restart your Spring Boot server, log in to get a fresh token from the new persistent key, and your event creation will work perfectly without any signature mismatches.
