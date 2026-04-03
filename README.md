  Executing task: cd server && mvn spring-boot:run -Dspring-boot.run.arguments="--server.port=3000 --MYSQL_CONNECTION_USER=root --MYSQL_CONNECTION_PASSWORD=root --MYSQL_CONNECTION_URL=jdbc:mysql://localhost:3306/mydb" -Dmaven.test.skip=true 

[INFO] Scanning for projects...
[INFO] 
[INFO] ----------------< com.edutech:Event-Management-system >-----------------
[INFO] Building logistics-management-and-tracking-system 0.0.1-SNAPSHOT
[INFO] --------------------------------[ jar ]---------------------------------
[INFO] 
[INFO] >>> spring-boot-maven-plugin:2.7.17:run (default-cli) > test-compile @ Event-Management-system >>>
[INFO] 
[INFO] --- maven-resources-plugin:3.2.0:resources (default-resources) @ Event-Management-system ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] Using 'UTF-8' encoding to copy filtered properties files.
[INFO] Copying 1 resource
[INFO] Copying 0 resource
[INFO] 
[INFO] --- maven-compiler-plugin:3.10.1:compile (default-compile) @ Event-Management-system ---
[INFO] Nothing to compile - all classes are up to date
[INFO] 
[INFO] --- maven-resources-plugin:3.2.0:testResources (default-testResources) @ Event-Management-system ---
[INFO] Not copying test resources
[INFO] 
[INFO] --- maven-compiler-plugin:3.10.1:testCompile (default-testCompile) @ Event-Management-system ---
[INFO] Not compiling test sources
[INFO] 
[INFO] <<< spring-boot-maven-plugin:2.7.17:run (default-cli) < test-compile @ Event-Management-system <<<
[INFO] 
[INFO] 
[INFO] --- spring-boot-maven-plugin:2.7.17:run (default-cli) @ Event-Management-system ---
[INFO] Attaching agents: []
20:41:11.679 [Thread-0] DEBUG org.springframework.boot.devtools.restart.classloader.RestartClassLoader - Created RestartClassLoader org.springframework.boot.devtools.restart.classloader.RestartClassLoader@75858956

  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::               (v2.7.17)

2026-04-03 20:41:12.022  INFO 3217 --- [  restartedMain] c.e.e.EventManagementSystemApplication   : Starting EventManagementSystemApplication using Java 21.0.7 on ed107dfcd815 with PID 3217 (/home/coder/app/server/target/classes started by coder in /home/coder/app/server)
2026-04-03 20:41:12.023  INFO 3217 --- [  restartedMain] c.e.e.EventManagementSystemApplication   : No active profile set, falling back to 1 default profile: "default"
2026-04-03 20:41:12.064  INFO 3217 --- [  restartedMain] .e.DevToolsPropertyDefaultsPostProcessor : Devtools property defaults active! Set 'spring.devtools.add-properties' to 'false' to disable
2026-04-03 20:41:12.064  INFO 3217 --- [  restartedMain] .e.DevToolsPropertyDefaultsPostProcessor : For additional web related logging consider setting the 'logging.level.web' property to 'DEBUG'
2026-04-03 20:41:12.836  INFO 3217 --- [  restartedMain] .s.d.r.c.RepositoryConfigurationDelegate : Bootstrapping Spring Data JPA repositories in DEFAULT mode.
2026-04-03 20:41:13.109  INFO 3217 --- [  restartedMain] .s.d.r.c.RepositoryConfigurationDelegate : Finished Spring Data repository scanning in 267 ms. Found 5 JPA repository interfaces.
2026-04-03 20:41:13.571  INFO 3217 --- [  restartedMain] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat initialized with port(s): 3000 (http)
2026-04-03 20:41:13.579  INFO 3217 --- [  restartedMain] o.apache.catalina.core.StandardService   : Starting service [Tomcat]
2026-04-03 20:41:13.579  INFO 3217 --- [  restartedMain] org.apache.catalina.core.StandardEngine  : Starting Servlet engine: [Apache Tomcat/9.0.82]
2026-04-03 20:41:13.631  INFO 3217 --- [  restartedMain] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring embedded WebApplicationContext
2026-04-03 20:41:13.631  INFO 3217 --- [  restartedMain] w.s.c.ServletWebServerApplicationContext : Root WebApplicationContext: initialization completed in 1567 ms
2026-04-03 20:41:13.664  INFO 3217 --- [  restartedMain] com.zaxxer.hikari.HikariDataSource       : HikariPool-1 - Starting...
2026-04-03 20:41:13.887  INFO 3217 --- [  restartedMain] com.zaxxer.hikari.HikariDataSource       : HikariPool-1 - Start completed.
2026-04-03 20:41:13.893  INFO 3217 --- [  restartedMain] o.s.b.a.h2.H2ConsoleAutoConfiguration    : H2 console available at '/h2-console'. Database available at 'jdbc:mysql://localhost:3306/mydb'
2026-04-03 20:41:14.108  INFO 3217 --- [  restartedMain] o.hibernate.jpa.internal.util.LogHelper  : HHH000204: Processing PersistenceUnitInfo [name: default]
2026-04-03 20:41:14.134  INFO 3217 --- [  restartedMain] org.hibernate.Version                    : HHH000412: Hibernate ORM core version 5.6.15.Final
2026-04-03 20:41:14.249  INFO 3217 --- [  restartedMain] o.hibernate.annotations.common.Version   : HCANN000001: Hibernate Commons Annotations {5.1.2.Final}
2026-04-03 20:41:14.313  INFO 3217 --- [  restartedMain] org.hibernate.dialect.Dialect            : HHH000400: Using dialect: org.hibernate.dialect.MySQL5Dialect
2026-04-03 20:41:14.783  INFO 3217 --- [  restartedMain] o.h.e.t.j.p.i.JtaPlatformInitiator       : HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
2026-04-03 20:41:14.789  INFO 3217 --- [  restartedMain] j.LocalContainerEntityManagerFactoryBean : Initialized JPA EntityManagerFactory for persistence unit 'default'
2026-04-03 20:41:15.078  WARN 3217 --- [  restartedMain] JpaBaseConfiguration$JpaWebConfiguration : spring.jpa.open-in-view is enabled by default. Therefore, database queries may be performed during view rendering. Explicitly configure spring.jpa.open-in-view to disable this warning
2026-04-03 20:41:15.257  INFO 3217 --- [  restartedMain] o.s.s.web.DefaultSecurityFilterChain     : Will secure any request with [org.springframework.security.web.session.DisableEncodeUrlFilter@75386538, org.springframework.security.web.context.request.async.WebAsyncManagerIntegrationFilter@28622111, org.springframework.security.web.context.SecurityContextPersistenceFilter@7a3ba469, org.springframework.security.web.header.HeaderWriterFilter@2fbee7a3, org.springframework.security.web.authentication.logout.LogoutFilter@4e9f2428, com.edutech.eventmanagementsystem.jwt.JwtRequestFilter@20d34272, org.springframework.security.web.savedrequest.RequestCacheAwareFilter@55730fab, org.springframework.security.web.servletapi.SecurityContextHolderAwareRequestFilter@58284d01, org.springframework.security.web.authentication.AnonymousAuthenticationFilter@322ff51d, org.springframework.security.web.session.SessionManagementFilter@13382b91, org.springframework.security.web.access.ExceptionTranslationFilter@4154c4a2, org.springframework.security.web.access.intercept.FilterSecurityInterceptor@7f7b4109]
2026-04-03 20:41:15.766  INFO 3217 --- [  restartedMain] o.s.b.d.a.OptionalLiveReloadServer       : LiveReload server is running on port 35729
2026-04-03 20:41:15.785  INFO 3217 --- [  restartedMain] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port(s): 3000 (http) with context path ''
2026-04-03 20:41:15.791  INFO 3217 --- [  restartedMain] c.e.e.EventManagementSystemApplication   : Started EventManagementSystemApplication in 4.101 seconds (JVM running for 4.421)
2026-04-03 20:41:19.704  INFO 3217 --- [nio-3000-exec-1] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring DispatcherServlet 'dispatcherServlet'
2026-04-03 20:41:19.704  INFO 3217 --- [nio-3000-exec-1] o.s.web.servlet.DispatcherServlet        : Initializing Servlet 'dispatcherServlet'
2026-04-03 20:41:19.704  INFO 3217 --- [nio-3000-exec-1] o.s.web.servlet.DispatcherServlet        : Completed initialization in 0 ms
2026-04-03 20:41:21.707  WARN 3217 --- [nio-3000-exec-2] o.h.engine.jdbc.spi.SqlExceptionHelper   : SQL Error: 1364, SQLState: HY000
2026-04-03 20:41:21.707 ERROR 3217 --- [nio-3000-exec-2] o.h.engine.jdbc.spi.SqlExceptionHelper   : Field 'id' doesn't have a default value
2026-04-03 20:41:21.730 ERROR 3217 --- [nio-3000-exec-2] o.a.c.c.C.[.[.[/].[dispatcherServlet]    : Servlet.service() for servlet [dispatcherServlet] in context with path [] threw exception [Request processing failed; nested exception is org.springframework.orm.jpa.JpaSystemException: could not execute statement; nested exception is org.hibernate.exception.GenericJDBCException: could not execute statement] with root cause

java.sql.SQLException: Field 'id' doesn't have a default value
        at com.mysql.cj.jdbc.exceptions.SQLError.createSQLException(SQLError.java:130) ~[mysql-connector-j-8.0.33.jar:8.0.33]
        at com.mysql.cj.jdbc.exceptions.SQLExceptionsMapping.translateException(SQLExceptionsMapping.java:122) ~[mysql-connector-j-8.0.33.jar:8.0.33]
        at com.mysql.cj.jdbc.ClientPreparedStatement.executeInternal(ClientPreparedStatement.java:916) ~[mysql-connector-j-8.0.33.jar:8.0.33]
        at com.mysql.cj.jdbc.ClientPreparedStatement.executeUpdateInternal(ClientPreparedStatement.java:1061) ~[mysql-connector-j-8.0.33.jar:8.0.33]
        at com.mysql.cj.jdbc.ClientPreparedStatement.executeUpdateInternal(ClientPreparedStatement.java:1009) ~[mysql-connector-j-8.0.33.jar:8.0.33]
        at com.mysql.cj.jdbc.ClientPreparedStatement.executeLargeUpdate(ClientPreparedStatement.java:1320) ~[mysql-connector-j-8.0.33.jar:8.0.33]
        at com.mysql.cj.jdbc.ClientPreparedStatement.executeUpdate(ClientPreparedStatement.java:994) ~[mysql-connector-j-8.0.33.jar:8.0.33]
        at com.zaxxer.hikari.pool.ProxyPreparedStatement.executeUpdate(ProxyPreparedStatement.java:61) ~[HikariCP-4.0.3.jar:na]
        at com.zaxxer.hikari.pool.HikariProxyPreparedStatement.executeUpdate(HikariProxyPreparedStatement.java) ~[HikariCP-4.0.3.jar:na]
        at org.hibernate.engine.jdbc.internal.ResultSetReturnImpl.executeUpdate(ResultSetReturnImpl.java:197) ~[hibernate-core-5.6.15.Final.jar:5.6.15.Final]
        at org.hibernate.dialect.identity.GetGeneratedKeysDelegate.executeAndExtract(GetGeneratedKeysDelegate.java:58) ~[hibernate-core-5.6.15.Final.jar:5.6.15.Final]
        at org.hibernate.id.insert.AbstractReturningDelegate.performInsert(AbstractReturningDelegate.java:43) ~[hibernate-core-5.6.15.Final.jar:5.6.15.Final]
        at org.hibernate.persister.entity.AbstractEntityPersister.insert(AbstractEntityPersister.java:3279) ~[hibernate-core-5.6.15.Final.jar:5.6.15.Final]
        at org.hibernate.persister.entity.AbstractEntityPersister.insert(AbstractEntityPersister.java:3914) ~[hibernate-core-5.6.15.Final.jar:5.6.15.Final]
        at org.hibernate.action.internal.EntityIdentityInsertAction.execute(EntityIdentityInsertAction.java:84) ~[hibernate-core-5.6.15.Final.jar:5.6.15.Final]
        at org.hibernate.engine.spi.ActionQueue.execute(ActionQueue.java:645) ~[hibernate-core-5.6.15.Final.jar:5.6.15.Final]
        at org.hibernate.engine.spi.ActionQueue.addResolvedEntityInsertAction(ActionQueue.java:282) ~[hibernate-core-5.6.15.Final.jar:5.6.15.Final]
        at org.hibernate.engine.spi.ActionQueue.addInsertAction(ActionQueue.java:263) ~[hibernate-core-5.6.15.Final.jar:5.6.15.Final]
        at org.hibernate.engine.spi.ActionQueue.addAction(ActionQueue.java:317) ~[hibernate-core-5.6.15.Final.jar:5.6.15.Final]
        at org.hibernate.event.internal.AbstractSaveEventListener.addInsertAction(AbstractSaveEventListener.java:329) ~[hibernate-core-5.6.15.Final.jar:5.6.15.Final]
        at org.hibernate.event.internal.AbstractSaveEventListener.performSaveOrReplicate(AbstractSaveEventListener.java:286) ~[hibernate-core-5.6.15.Final.jar:5.6.15.Final]
        at org.hibernate.event.internal.AbstractSaveEventListener.performSave(AbstractSaveEventListener.java:192) ~[hibernate-core-5.6.15.Final.jar:5.6.15.Final]
        at org.hibernate.event.internal.AbstractSaveEventListener.saveWithGeneratedId(AbstractSaveEventListener.java:122) ~[hibernate-core-5.6.15.Final.jar:5.6.15.Final]
        at org.hibernate.event.internal.DefaultPersistEventListener.entityIsTransient(DefaultPersistEventListener.java:185) ~[hibernate-core-5.6.15.Final.jar:5.6.15.Final]
        at org.hibernate.event.internal.DefaultPersistEventListener.onPersist(DefaultPersistEventListener.java:128) ~[hibernate-core-5.6.15.Final.jar:5.6.15.Final]
        at org.hibernate.event.internal.DefaultPersistEventListener.onPersist(DefaultPersistEventListener.java:55) ~[hibernate-core-5.6.15.Final.jar:5.6.15.Final]
        at org.hibernate.event.service.internal.EventListenerGroupImpl.fireEventOnEachListener(EventListenerGroupImpl.java:107) ~[hibernate-core-5.6.15.Final.jar:5.6.15.Final]
        at org.hibernate.internal.SessionImpl.firePersist(SessionImpl.java:756) ~[hibernate-core-5.6.15.Final.jar:5.6.15.Final]
        at org.hibernate.internal.SessionImpl.persist(SessionImpl.java:742) ~[hibernate-core-5.6.15.Final.jar:5.6.15.Final]
        at java.base/jdk.internal.reflect.DirectMethodHandleAccessor.invoke(DirectMethodHandleAccessor.java:103) ~[na:na]
        at java.base/java.lang.reflect.Method.invoke(Method.java:580) ~[na:na]
        at org.springframework.orm.jpa.ExtendedEntityManagerCreator$ExtendedEntityManagerInvocationHandler.invoke(ExtendedEntityManagerCreator.java:362) ~[spring-orm-5.3.30.jar:5.3.30]
        at jdk.proxy4/jdk.proxy4.$Proxy110.persist(Unknown Source) ~[na:na]
        at java.base/jdk.internal.reflect.DirectMethodHandleAccessor.invoke(DirectMethodHandleAccessor.java:103) ~[na:na]
        at java.base/java.lang.reflect.Method.invoke(Method.java:580) ~[na:na]
        at org.springframework.orm.jpa.SharedEntityManagerCreator$SharedEntityManagerInvocationHandler.invoke(SharedEntityManagerCreator.java:315) ~[spring-orm-5.3.30.jar:5.3.30]
        at jdk.proxy4/jdk.proxy4.$Proxy110.persist(Unknown Source) ~[na:na]
        at org.springframework.data.jpa.repository.support.SimpleJpaRepository.save(SimpleJpaRepository.java:666) ~[spring-data-jpa-2.7.17.jar:2.7.17]
        at java.base/jdk.internal.reflect.DirectMethodHandleAccessor.invoke(DirectMethodHandleAccessor.java:103) ~[na:na]
        at java.base/java.lang.reflect.Method.invoke(Method.java:580) ~[na:na]
        at org.springframework.data.repository.core.support.RepositoryMethodInvoker$RepositoryFragmentMethodInvoker.lambda$new$0(RepositoryMethodInvoker.java:289) ~[spring-data-commons-2.7.17.jar:2.7.17]
        at org.springframework.data.repository.core.support.RepositoryMethodInvoker.doInvoke(RepositoryMethodInvoker.java:137) ~[spring-data-commons-2.7.17.jar:2.7.17]
        at org.springframework.data.repository.core.support.RepositoryMethodInvoker.invoke(RepositoryMethodInvoker.java:121) ~[spring-data-commons-2.7.17.jar:2.7.17]
        at org.springframework.data.repository.core.support.RepositoryComposition$RepositoryFragments.invoke(RepositoryComposition.java:530) ~[spring-data-commons-2.7.17.jar:2.7.17]
        at org.springframework.data.repository.core.support.RepositoryComposition.invoke(RepositoryComposition.java:286) ~[spring-data-commons-2.7.17.jar:2.7.17]
        at org.springframework.data.repository.core.support.RepositoryFactorySupport$ImplementationMethodExecutionInterceptor.invoke(RepositoryFactorySupport.java:640) ~[spring-data-commons-2.7.17.jar:2.7.17]
        at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:186) ~[spring-aop-5.3.30.jar:5.3.30]
        at org.springframework.data.repository.core.support.QueryExecutorMethodInterceptor.doInvoke(QueryExecutorMethodInterceptor.java:164) ~[spring-data-commons-2.7.17.jar:2.7.17]
        at org.springframework.data.repository.core.support.QueryExecutorMethodInterceptor.invoke(QueryExecutorMethodInterceptor.java:139) ~[spring-data-commons-2.7.17.jar:2.7.17]
        at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:186) ~[spring-aop-5.3.30.jar:5.3.30]
        at org.springframework.data.projection.DefaultMethodInvokingMethodInterceptor.invoke(DefaultMethodInvokingMethodInterceptor.java:76) ~[spring-data-commons-2.7.17.jar:2.7.17]
        at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:186) ~[spring-aop-5.3.30.jar:5.3.30]
        at org.springframework.transaction.interceptor.TransactionInterceptor$1.proceedWithInvocation(TransactionInterceptor.java:123) ~[spring-tx-5.3.30.jar:5.3.30]
        at org.springframework.transaction.interceptor.TransactionAspectSupport.invokeWithinTransaction(TransactionAspectSupport.java:388) ~[spring-tx-5.3.30.jar:5.3.30]
        at org.springframework.transaction.interceptor.TransactionInterceptor.invoke(TransactionInterceptor.java:119) ~[spring-tx-5.3.30.jar:5.3.30]
        at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:186) ~[spring-aop-5.3.30.jar:5.3.30]
        at org.springframework.dao.support.PersistenceExceptionTranslationInterceptor.invoke(PersistenceExceptionTranslationInterceptor.java:137) ~[spring-tx-5.3.30.jar:5.3.30]
        at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:186) ~[spring-aop-5.3.30.jar:5.3.30]
        at org.springframework.data.jpa.repository.support.CrudMethodMetadataPostProcessor$CrudMethodMetadataPopulatingMethodInterceptor.invoke(CrudMethodMetadataPostProcessor.java:174) ~[spring-data-jpa-2.7.17.jar:2.7.17]
        at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:186) ~[spring-aop-5.3.30.jar:5.3.30]
        at org.springframework.aop.interceptor.ExposeInvocationInterceptor.invoke(ExposeInvocationInterceptor.java:97) ~[spring-aop-5.3.30.jar:5.3.30]
        at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:186) ~[spring-aop-5.3.30.jar:5.3.30]
        at org.springframework.aop.framework.JdkDynamicAopProxy.invoke(JdkDynamicAopProxy.java:241) ~[spring-aop-5.3.30.jar:5.3.30]
        at jdk.proxy4/jdk.proxy4.$Proxy120.save(Unknown Source) ~[na:na]
        at com.edutech.eventmanagementsystem.service.EventService.createEvent(EventService.java:19) ~[classes/:na]
        at com.edutech.eventmanagementsystem.controller.EventPlannerController.createEvent(EventPlannerController.java:27) ~[classes/:na]
        at java.base/jdk.internal.reflect.DirectMethodHandleAccessor.invoke(DirectMethodHandleAccessor.java:103) ~[na:na]
        at java.base/java.lang.reflect.Method.invoke(Method.java:580) ~[na:na]
        at org.springframework.web.method.support.InvocableHandlerMethod.doInvoke(InvocableHandlerMethod.java:205) ~[spring-web-5.3.30.jar:5.3.30]
        at org.springframework.web.method.support.InvocableHandlerMethod.invokeForRequest(InvocableHandlerMethod.java:150) ~[spring-web-5.3.30.jar:5.3.30]
        at org.springframework.web.servlet.mvc.method.annotation.ServletInvocableHandlerMethod.invokeAndHandle(ServletInvocableHandlerMethod.java:117) ~[spring-webmvc-5.3.30.jar:5.3.30]
        at org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerAdapter.invokeHandlerMethod(RequestMappingHandlerAdapter.java:895) ~[spring-webmvc-5.3.30.jar:5.3.30]
        at org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerAdapter.handleInternal(RequestMappingHandlerAdapter.java:808) ~[spring-webmvc-5.3.30.jar:5.3.30]
        at org.springframework.web.servlet.mvc.method.AbstractHandlerMethodAdapter.handle(AbstractHandlerMethodAdapter.java:87) ~[spring-webmvc-5.3.30.jar:5.3.30]
        at org.springframework.web.servlet.DispatcherServlet.doDispatch(DispatcherServlet.java:1072) ~[spring-webmvc-5.3.30.jar:5.3.30]
        at org.springframework.web.servlet.DispatcherServlet.doService(DispatcherServlet.java:965) ~[spring-webmvc-5.3.30.jar:5.3.30]
        at org.springframework.web.servlet.FrameworkServlet.processRequest(FrameworkServlet.java:1006) ~[spring-webmvc-5.3.30.jar:5.3.30]
        at org.springframework.web.servlet.FrameworkServlet.doPost(FrameworkServlet.java:909) ~[spring-webmvc-5.3.30.jar:5.3.30]
        at javax.servlet.http.HttpServlet.service(HttpServlet.java:555) ~[tomcat-embed-core-9.0.82.jar:4.0.FR]
        at org.springframework.web.servlet.FrameworkServlet.service(FrameworkServlet.java:883) ~[spring-webmvc-5.3.30.jar:5.3.30]
        at javax.servlet.http.HttpServlet.service(HttpServlet.java:623) ~[tomcat-embed-core-9.0.82.jar:4.0.FR]
        at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:209) ~[tomcat-embed-core-9.0.82.jar:9.0.82]
        at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:153) ~[tomcat-embed-core-9.0.82.jar:9.0.82]
        at org.apache.tomcat.websocket.server.WsFilter.doFilter(WsFilter.java:51) ~[tomcat-embed-websocket-9.0.82.jar:9.0.82]
        at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:178) ~[tomcat-embed-core-9.0.82.jar:9.0.82]
        at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:153) ~[tomcat-embed-core-9.0.82.jar:9.0.82]
        at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:111) ~[spring-web-5.3.30.jar:5.3.30]
        at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:178) ~[tomcat-embed-core-9.0.82.jar:9.0.82]
        at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:153) ~[tomcat-embed-core-9.0.82.jar:9.0.82]
        at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:337) ~[spring-security-web-5.7.11.jar:5.7.11]
        at org.springframework.security.web.access.intercept.FilterSecurityInterceptor.invoke(FilterSecurityInterceptor.java:115) ~[spring-security-web-5.7.11.jar:5.7.11]
        at org.springframework.security.web.access.intercept.FilterSecurityInterceptor.doFilter(FilterSecurityInterceptor.java:81) ~[spring-security-web-5.7.11.jar:5.7.11]
        at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:346) ~[spring-security-web-5.7.11.jar:5.7.11]
        at org.springframework.security.web.access.ExceptionTranslationFilter.doFilter(ExceptionTranslationFilter.java:122) ~[spring-security-web-5.7.11.jar:5.7.11]
        at org.springframework.security.web.access.ExceptionTranslationFilter.doFilter(ExceptionTranslationFilter.java:116) ~[spring-security-web-5.7.11.jar:5.7.11]
        at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:346) ~[spring-security-web-5.7.11.jar:5.7.11]
        at org.springframework.security.web.session.SessionManagementFilter.doFilter(SessionManagementFilter.java:126) ~[spring-security-web-5.7.11.jar:5.7.11]
        at org.springframework.security.web.session.SessionManagementFilter.doFilter(SessionManagementFilter.java:81) ~[spring-security-web-5.7.11.jar:5.7.11]
        at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:346) ~[spring-security-web-5.7.11.jar:5.7.11]
        at org.springframework.security.web.authentication.AnonymousAuthenticationFilter.doFilter(AnonymousAuthenticationFilter.java:109) ~[spring-security-web-5.7.11.jar:5.7.11]
        at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:346) ~[spring-security-web-5.7.11.jar:5.7.11]
        at org.springframework.security.web.servletapi.SecurityContextHolderAwareRequestFilter.doFilter(SecurityContextHolderAwareRequestFilter.java:149) ~[spring-security-web-5.7.11.jar:5.7.11]
        at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:346) ~[spring-security-web-5.7.11.jar:5.7.11]
        at org.springframework.security.web.savedrequest.RequestCacheAwareFilter.doFilter(RequestCacheAwareFilter.java:63) ~[spring-security-web-5.7.11.jar:5.7.11]
        at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:346) ~[spring-security-web-5.7.11.jar:5.7.11]
        at com.edutech.eventmanagementsystem.jwt.JwtRequestFilter.doFilterInternal(JwtRequestFilter.java:56) ~[classes/:na]
        at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:117) ~[spring-web-5.3.30.jar:5.3.30]
        at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:346) ~[spring-security-web-5.7.11.jar:5.7.11]
        at org.springframework.security.web.authentication.logout.LogoutFilter.doFilter(LogoutFilter.java:103) ~[spring-security-web-5.7.11.jar:5.7.11]
        at org.springframework.security.web.authentication.logout.LogoutFilter.doFilter(LogoutFilter.java:89) ~[spring-security-web-5.7.11.jar:5.7.11]
        at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:346) ~[spring-security-web-5.7.11.jar:5.7.11]
        at org.springframework.security.web.header.HeaderWriterFilter.doHeadersAfter(HeaderWriterFilter.java:90) ~[spring-security-web-5.7.11.jar:5.7.11]
        at org.springframework.security.web.header.HeaderWriterFilter.doFilterInternal(HeaderWriterFilter.java:75) ~[spring-security-web-5.7.11.jar:5.7.11]
        at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:117) ~[spring-web-5.3.30.jar:5.3.30]
        at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:346) ~[spring-security-web-5.7.11.jar:5.7.11]
        at org.springframework.security.web.context.SecurityContextPersistenceFilter.doFilter(SecurityContextPersistenceFilter.java:112) ~[spring-security-web-5.7.11.jar:5.7.11]
        at org.springframework.security.web.context.SecurityContextPersistenceFilter.doFilter(SecurityContextPersistenceFilter.java:82) ~[spring-security-web-5.7.11.jar:5.7.11]
        at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:346) ~[spring-security-web-5.7.11.jar:5.7.11]
        at org.springframework.security.web.context.request.async.WebAsyncManagerIntegrationFilter.doFilterInternal(WebAsyncManagerIntegrationFilter.java:55) ~[spring-security-web-5.7.11.jar:5.7.11]
        at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:117) ~[spring-web-5.3.30.jar:5.3.30]
        at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:346) ~[spring-security-web-5.7.11.jar:5.7.11]
        at org.springframework.security.web.session.DisableEncodeUrlFilter.doFilterInternal(DisableEncodeUrlFilter.java:42) ~[spring-security-web-5.7.11.jar:5.7.11]
        at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:117) ~[spring-web-5.3.30.jar:5.3.30]
        at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:346) ~[spring-security-web-5.7.11.jar:5.7.11]
        at org.springframework.security.web.FilterChainProxy.doFilterInternal(FilterChainProxy.java:221) ~[spring-security-web-5.7.11.jar:5.7.11]
        at org.springframework.security.web.FilterChainProxy.doFilter(FilterChainProxy.java:186) ~[spring-security-web-5.7.11.jar:5.7.11]
        at org.springframework.web.filter.DelegatingFilterProxy.invokeDelegate(DelegatingFilterProxy.java:354) ~[spring-web-5.3.30.jar:5.3.30]
        at org.springframework.web.filter.DelegatingFilterProxy.doFilter(DelegatingFilterProxy.java:267) ~[spring-web-5.3.30.jar:5.3.30]
        at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:178) ~[tomcat-embed-core-9.0.82.jar:9.0.82]
        at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:153) ~[tomcat-embed-core-9.0.82.jar:9.0.82]
        at org.springframework.web.filter.RequestContextFilter.doFilterInternal(RequestContextFilter.java:100) ~[spring-web-5.3.30.jar:5.3.30]
        at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:117) ~[spring-web-5.3.30.jar:5.3.30]
        at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:178) ~[tomcat-embed-core-9.0.82.jar:9.0.82]
        at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:153) ~[tomcat-embed-core-9.0.82.jar:9.0.82]
        at org.springframework.web.filter.FormContentFilter.doFilterInternal(FormContentFilter.java:93) ~[spring-web-5.3.30.jar:5.3.30]
        at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:117) ~[spring-web-5.3.30.jar:5.3.30]
        at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:178) ~[tomcat-embed-core-9.0.82.jar:9.0.82]
        at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:153) ~[tomcat-embed-core-9.0.82.jar:9.0.82]
        at org.springframework.web.filter.CharacterEncodingFilter.doFilterInternal(CharacterEncodingFilter.java:201) ~[spring-web-5.3.30.jar:5.3.30]
        at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:117) ~[spring-web-5.3.30.jar:5.3.30]
        at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:178) ~[tomcat-embed-core-9.0.82.jar:9.0.82]
        at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:153) ~[tomcat-embed-core-9.0.82.jar:9.0.82]
        at org.apache.catalina.core.StandardWrapperValve.invoke(StandardWrapperValve.java:168) ~[tomcat-embed-core-9.0.82.jar:9.0.82]
        at org.apache.catalina.core.StandardContextValve.invoke(StandardContextValve.java:90) ~[tomcat-embed-core-9.0.82.jar:9.0.82]
        at org.apache.catalina.authenticator.AuthenticatorBase.invoke(AuthenticatorBase.java:481) ~[tomcat-embed-core-9.0.82.jar:9.0.82]
        at org.apache.catalina.core.StandardHostValve.invoke(StandardHostValve.java:130) ~[tomcat-embed-core-9.0.82.jar:9.0.82]
        at org.apache.catalina.valves.ErrorReportValve.invoke(ErrorReportValve.java:93) ~[tomcat-embed-core-9.0.82.jar:9.0.82]
        at org.apache.catalina.core.StandardEngineValve.invoke(StandardEngineValve.java:74) ~[tomcat-embed-core-9.0.82.jar:9.0.82]
        at org.apache.catalina.connector.CoyoteAdapter.service(CoyoteAdapter.java:342) ~[tomcat-embed-core-9.0.82.jar:9.0.82]
        at org.apache.coyote.http11.Http11Processor.service(Http11Processor.java:390) ~[tomcat-embed-core-9.0.82.jar:9.0.82]
        at org.apache.coyote.AbstractProcessorLight.process(AbstractProcessorLight.java:63) ~[tomcat-embed-core-9.0.82.jar:9.0.82]
        at org.apache.coyote.AbstractProtocol$ConnectionHandler.process(AbstractProtocol.java:928) ~[tomcat-embed-core-9.0.82.jar:9.0.82]
        at org.apache.tomcat.util.net.NioEndpoint$SocketProcessor.doRun(NioEndpoint.java:1794) ~[tomcat-embed-core-9.0.82.jar:9.0.82]
        at org.apache.tomcat.util.net.SocketProcessorBase.run(SocketProcessorBase.java:52) ~[tomcat-embed-core-9.0.82.jar:9.0.82]
        at org.apache.tomcat.util.threads.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1191) ~[tomcat-embed-core-9.0.82.jar:9.0.82]
        at org.apache.tomcat.util.threads.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:659) ~[tomcat-embed-core-9.0.82.jar:9.0.82]
        at org.apache.tomcat.util.threads.TaskThread$WrappingRunnable.run(TaskThread.java:61) ~[tomcat-embed-core-9.0.82.jar:9.0.82]
        at java.base/java.lang.Thread.run(Thread.java:1583) ~[na:na]
