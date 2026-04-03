To elevate EventMaster Pro from a standard capstone project to a production-ready application, the dashboard needs to act as a dynamic, role-based command center. Instead of just showing a static welcome screen, it should immediately surface actionable insights (KPIs) and provide a polished, modern UI that fits a premium event management theme (deep blues, gold accents, and clean card layouts).
Here are the new features we are adding directly into the Dashboard:
 * Role-Based KPI Cards: Planners will instantly see 'Total Active Events' and 'Total Resources Inventory'. Clients will see 'Upcoming Events Available'.
 * Quick Action Hub: One-click routing to the most common tasks (Create Event, Allocate Resources, Live Ticketing) so users don't have to hunt through menus.
 * Event Countdown / Highlight Reel: A visual feed of the latest events pulled dynamically from the database.
Here is the complete code to upgrade the Dashboard module.
1. dashbaord.component.ts (The Logic Layer)
Location: client/src/app/dashbaord/dashbaord.component.ts
We are adding reactive data fetching to calculate the KPI numbers on the fly.
import { Component, OnInit } from '@angular/core';
import { AuthService } from '../../services/auth.service';
import { HttpService } from '../../services/http.service';
import { Router } from '@angular/router';

@Component({
  selector: 'app-dashbaord',
  templateUrl: './dashbaord.component.html',
  styleUrls: ['./dashbaord.component.scss']
})
export class DashbaordComponent implements OnInit {
  role: string | null = '';
  username: string | null = '';
  
  // KPI Metrics
  totalEvents: number = 0;
  totalResources: number = 0;
  recentEvents: any[] = [];

  constructor(
    private authService: AuthService, 
    private httpService: HttpService,
    private router: Router
  ) {}

  ngOnInit(): void {
    this.role = this.authService.getRole();
    // Assuming the username is stored in local storage during login, otherwise default to role
    this.username = localStorage.getItem('username') || this.role; 

    this.loadDashboardData();
  }

  loadDashboardData(): void {
    const currentRole = this.role?.toUpperCase();

    if (currentRole === 'PLANNER') {
      this.httpService.GetAllevents().subscribe((events: any[]) => {
        this.totalEvents = events ? events.length : 0;
        // Grab the 3 most recent events for the highlight reel
        this.recentEvents = events ? events.slice(-3).reverse() : []; 
      });

      this.httpService.GetAllResources().subscribe((resources: any[]) => {
        this.totalResources = resources ? resources.length : 0;
      });
    } 
    else if (currentRole === 'CLIENT') {
      this.httpService.getActiveEvents().subscribe((events: any[]) => {
        this.totalEvents = events ? events.length : 0;
        this.recentEvents = events ? events.slice(0, 3) : [];
      });
    }
  }

  navigateTo(route: string): void {
    this.router.navigate([`/${route}`]);
  }
}

2. dashbaord.component.html (The Themed UI)
Location: client/src/app/dashbaord/dashbaord.component.html
This implements a responsive CSS Grid with a premium look and feel.
<div class="dashboard-container">
  <header class="dashboard-hero">
    <div class="hero-content">
      <h1>Welcome back, <span class="highlight">{{ username | titlecase }}</span>!</h1>
      <p *ngIf="role === 'PLANNER'">Your command center for EventMaster Pro. All systems go.</p>
      <p *ngIf="role === 'CLIENT'">Discover and book your next unforgettable experience.</p>
      <p *ngIf="role === 'STAFF'">View your upcoming venue setups and task allocations.</p>
    </div>
  </header>

  <section class="kpi-grid" *ngIf="role === 'PLANNER' || role === 'CLIENT'">
    <div class="kpi-card">
      <div class="kpi-icon">📅</div>
      <div class="kpi-data">
        <h3>{{ role === 'PLANNER' ? 'Total Events' : 'Available Events' }}</h3>
        <h2>{{ totalEvents }}</h2>
      </div>
    </div>

    <div class="kpi-card" *ngIf="role === 'PLANNER'">
      <div class="kpi-icon">📦</div>
      <div class="kpi-data">
        <h3>Resources Tracked</h3>
        <h2>{{ totalResources }}</h2>
      </div>
    </div>
  </section>

  <div class="dashboard-main">
    
    <aside class="quick-actions" *ngIf="role === 'PLANNER'">
      <h3>Quick Actions</h3>
      <button class="action-btn primary" (click)="navigateTo('create-event')">
        <span>➕</span> Create New Event
      </button>
      <button class="action-btn" (click)="navigateTo('add-resource')">
        <span>📥</span> Add Resource
      </button>
      <button class="action-btn" (click)="navigateTo('resource-allocate')">
        <span>🔗</span> Allocate Resources
      </button>
      <button class="action-btn alert" (click)="navigateTo('live-ticketing')">
        <span>📡</span> Live Ticketing Hub
      </button>
    </aside>

    <section class="highlight-reel" *ngIf="role === 'PLANNER' || role === 'CLIENT'">
      <h3>{{ role === 'PLANNER' ? 'Recently Created Events' : 'Trending Events' }}</h3>
      
      <div class="empty-state" *ngIf="recentEvents.length === 0">
        <p>No events found. Start building your portfolio!</p>
      </div>

      <div class="event-list">
        <div class="event-ticket" *ngFor="let event of recentEvents">
          <div class="ticket-date">
            <span class="month">{{ event.dateTime | date:'MMM' }}</span>
            <span class="day">{{ event.dateTime | date:'dd' }}</span>
          </div>
          <div class="ticket-info">
            <h4>{{ event.title }}</h4>
            <p>📍 {{ event.location }}</p>
            <span class="status-badge" [ngClass]="event.status?.toLowerCase()">
              {{ event.status || 'ACTIVE' }}
            </span>
          </div>
        </div>
      </div>
    </section>
  </div>
</div>

3. dashbaord.component.scss (The Premium Theme Styling)
Location: client/src/app/dashbaord/dashbaord.component.scss
This styling uses deep navy blues (#0B192C), crisp whites, and vibrant gold/blue accents to give it a professional event-management aesthetic.
.dashboard-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  color: #333;
}

.dashboard-hero {
  background: linear-gradient(135deg, #0B192C 0%, #1A365D 100%);
  color: white;
  padding: 3rem 2rem;
  border-radius: 12px;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.15);
  margin-bottom: 2rem;

  h1 {
    margin: 0;
    font-size: 2.5rem;
    font-weight: 700;
  }

  .highlight {
    color: #FACC15; /* Gold accent */
  }

  p {
    margin-top: 0.5rem;
    font-size: 1.1rem;
    opacity: 0.9;
  }
}

.kpi-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 1.5rem;
  margin-bottom: 2.5rem;

  .kpi-card {
    background: white;
    border-radius: 10px;
    padding: 1.5rem;
    display: flex;
    align-items: center;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
    border-left: 5px solid #2563EB;
    transition: transform 0.2s ease;

    &:hover {
      transform: translateY(-3px);
    }

    .kpi-icon {
      font-size: 2.5rem;
      margin-right: 1.5rem;
      background: #EFF6FF;
      padding: 1rem;
      border-radius: 50%;
    }

    .kpi-data {
      h3 { margin: 0; font-size: 0.9rem; color: #666; text-transform: uppercase; letter-spacing: 0.5px;}
      h2 { margin: 5px 0 0 0; font-size: 2rem; color: #0B192C; }
    }
  }
}

.dashboard-main {
  display: grid;
  grid-template-columns: 1fr 2fr;
  gap: 2rem;

  @media (max-width: 768px) {
    grid-template-columns: 1fr;
  }
}

.quick-actions {
  background: white;
  padding: 1.5rem;
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
  height: fit-content;

  h3 { margin-top: 0; margin-bottom: 1.5rem; color: #0B192C; border-bottom: 2px solid #F3F4F6; padding-bottom: 0.5rem;}

  .action-btn {
    display: flex;
    align-items: center;
    width: 100%;
    padding: 1rem;
    margin-bottom: 1rem;
    border: none;
    border-radius: 8px;
    background: #F8FAFC;
    color: #333;
    font-size: 1rem;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.2s ease;

    span { margin-right: 10px; font-size: 1.2rem; }

    &:hover { background: #E2E8F0; }
    
    &.primary {
      background: #2563EB; color: white;
      &:hover { background: #1D4ED8; }
    }

    &.alert {
      background: #FEF2F2; color: #DC2626; border: 1px solid #FECACA;
      &:hover { background: #FEE2E2; }
    }
  }
}

.highlight-reel {
  background: white;
  padding: 1.5rem;
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);

  h3 { margin-top: 0; margin-bottom: 1.5rem; color: #0B192C; }

  .empty-state {
    text-align: center; color: #64748B; padding: 2rem; background: #F8FAFC; border-radius: 8px; border: 1px dashed #CBD5E1;
  }

  .event-list {
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }

  .event-ticket {
    display: flex;
    border: 1px solid #E2E8F0;
    border-radius: 8px;
    overflow: hidden;
    transition: box-shadow 0.2s ease;

    &:hover { box-shadow: 0 4px 12px rgba(0,0,0,0.08); }

    .ticket-date {
      background: #F8FAFC;
      padding: 1rem 1.5rem;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      border-right: 2px dashed #CBD5E1;
      min-width: 80px;

      .month { color: #DC2626; font-weight: 700; font-size: 0.9rem; text-transform: uppercase;}
      .day { color: #0B192C; font-size: 1.8rem; font-weight: 800; line-height: 1;}
    }

    .ticket-info {
      padding: 1rem 1.5rem;
      flex-grow: 1;

      h4 { margin: 0 0 0.5rem 0; font-size: 1.1rem; color: #0B192C; }
      p { margin: 0 0 0.5rem 0; font-size: 0.9rem; color: #64748B; }

      .status-badge {
        display: inline-block;
        padding: 0.2rem 0.6rem;
        border-radius: 12px;
        font-size: 0.75rem;
        font-weight: 700;
        background: #DCFCE7;
        color: #166534;
        text-transform: uppercase;
      }
    }
  }
}

