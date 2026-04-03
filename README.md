This is music to a developer’s ears! Being freed from the constraints of rigid, outdated test cases means we can finally architect this application like a true, production-grade enterprise platform.
Instead of cramming everything into one messy "Dashboard" file with endless *ngIf statements, we are going to implement a Role-Based Micro-Frontend Architecture. We will completely delete the old dashboard and give each role their own dedicated files, styling, and landing pages.
Here is the complete blueprint to upgrade your app. We will do this in 4 Steps.
STEP 1: Routing & Global Navigation Update
First, we tell the Angular Router about our new pages, update the Login page to route users to their specific dashboards, and update the Global Header.
1. Update client/src/app/app-routing.module.ts
Replace your routes array to point to the new dashboards:
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
import { LoginComponent } from './login/login.component';
import { RegistrationComponent } from './registration/registration.component';
import { CreateEventComponent } from './create-event/create-event.component';
import { AddResourceComponent } from './add-resource/add-resource.component';
import { ResourceAllocateComponent } from './resource-allocate/resource-allocate.component';
import { ViewEventsComponent } from './view-events/view-events.component';
import { BookingDetailsComponent } from './booking-details/booking-details.component';
import { LiveTicketingComponent } from './live-ticketing/live-ticketing.component';

// NEW ROLE-BASED DASHBOARDS
import { PlannerDashboardComponent } from './planner-dashboard/planner-dashboard.component';
import { StaffDashboardComponent } from './staff-dashboard/staff-dashboard.component';
import { ClientDashboardComponent } from './client-dashboard/client-dashboard.component';

const routes: Routes = [
  { path: '', redirectTo: 'login', pathMatch: 'full' },
  { path: 'login', component: LoginComponent },
  { path: 'registration', component: RegistrationComponent },
  
  // Role Dashboards
  { path: 'planner-dashboard', component: PlannerDashboardComponent },
  { path: 'staff-dashboard', component: StaffDashboardComponent },
  { path: 'client-dashboard', component: ClientDashboardComponent },

  // Workspace Tools
  { path: 'create-event', component: CreateEventComponent },
  { path: 'add-resource', component: AddResourceComponent },
  { path: 'resource-allocate', component: ResourceAllocateComponent },
  { path: 'live-ticketing', component: LiveTicketingComponent },
  { path: 'view-events', component: ViewEventsComponent },
  { path: 'booking-details', component: BookingDetailsComponent },
  
  { path: '**', redirectTo: 'login' }
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }

2. Update client/src/app/app.module.ts
Add the new components to your declarations array. (You can remove DashbaordComponent since we are replacing it).
import { PlannerDashboardComponent } from './planner-dashboard/planner-dashboard.component';
import { StaffDashboardComponent } from './staff-dashboard/staff-dashboard.component';
import { ClientDashboardComponent } from './client-dashboard/client-dashboard.component';

// Inside @NgModule declarations array, add:
// PlannerDashboardComponent, StaffDashboardComponent, ClientDashboardComponent

3. Update client/src/app/login/login.component.ts
Find the onSubmit() method. When a user logs in, we now instantly redirect them to their custom dashboard!
  // Inside your login.component.ts -> onSubmit() method
  this.httpService.Login(this.itemForm.value).subscribe(
    (res: any) => {
      this.authService.setToken(res.token);
      this.authService.setRole(res.role);
      localStorage.setItem('username', this.itemForm.value.username);
      
      // THE FIX: Smart Routing!
      const role = res.role.toUpperCase();
      if (role === 'PLANNER') this.router.navigate(['/planner-dashboard']);
      else if (role === 'STAFF') this.router.navigate(['/staff-dashboard']);
      else if (role === 'CLIENT') this.router.navigate(['/client-dashboard']);
      else this.router.navigate(['/login']);
    },
    // ... error handling
  );

4. Update client/src/app/app.component.html (The Global Navbar)
Update the navigation links so the "Dashboard" button dynamically connects to the correct page, and the Logo routes to the correct home.
  <ng-container *ngIf="roleName === 'PLANNER'">
        <a routerLink="/planner-dashboard" routerLinkActive="active-link">Command Center</a>
        <a routerLink="/create-event" routerLinkActive="active-link">Events</a>
        <a routerLink="/add-resource" routerLinkActive="active-link">Inventory</a>
        <a routerLink="/resource-allocate" routerLinkActive="active-link">Allocation</a>
        <a routerLink="/live-ticketing" routerLinkActive="active-link">Live Ticketing</a>
      </ng-container>

      <ng-container *ngIf="roleName === 'STAFF'">
        <a routerLink="/staff-dashboard" routerLinkActive="active-link">Staff Home</a>
        <a routerLink="/view-events" routerLinkActive="active-link">Operations</a>
      </ng-container>

      <ng-container *ngIf="roleName === 'CLIENT'">
        <a routerLink="/client-dashboard" routerLinkActive="active-link">My Home</a>
        <a routerLink="/booking-details" routerLinkActive="active-link">Digital Passes</a>
      </ng-container>

STEP 2: The Planner Dashboard
Create a new folder: client/src/app/planner-dashboard.
planner-dashboard.component.ts:
import { Component, OnInit } from '@angular/core';
import { AuthService } from '../../services/auth.service';
import { HttpService } from '../../services/http.service';

@Component({
  selector: 'app-planner-dashboard',
  templateUrl: './planner-dashboard.component.html',
  styleUrls: ['./planner-dashboard.component.scss']
})
export class PlannerDashboardComponent implements OnInit {
  username: string = ''; lastLogin: Date = new Date();
  totalEvents = 0; ongoingEvents = 0; availableResources = 0; totalResources = 0; totalAllocations = 0;

  constructor(private authService: AuthService, private httpService: HttpService) {}

  ngOnInit(): void {
    this.username = localStorage.getItem('username') || 'Planner';
    const rawKey = 'previousLogin_' + this.username.toLowerCase();
    this.lastLogin = localStorage.getItem(rawKey) ? new Date(localStorage.getItem(rawKey)!) : new Date();

    this.httpService.GetAllevents().subscribe(data => {
      this.totalEvents = data.length;
      this.ongoingEvents = data.filter((e:any) => e.status?.toUpperCase() === 'ONGOING').length;
    });
    this.httpService.GetAllResources().subscribe(data => {
      this.totalResources = data.length;
      this.availableResources = data.filter((r:any) => r.availability).length;
    });
    this.httpService.getAllAllocations().subscribe(data => { this.totalAllocations = data.length; });
  }
}

planner-dashboard.component.html:
<div class="dashboard-wrapper">
  <header class="hero-banner planner-theme animate-slide-up">
    <div class="hero-content">
      <h1>EventMaster Command Center</h1>
      <p class="subtitle">Welcome back, {{ username | titlecase }}. System architecture is online.</p>
    </div>
  </header>

  <div class="dashboard-content animate-slide-up">
    <div class="section-title"><h3>Global Metrics</h3></div>
    <div class="metrics-grid">
      <div class="metric-card"><div class="metric-info"><h4>Total Events Hosted</h4><h2>{{ totalEvents }}</h2></div></div>
      <div class="metric-card highlight"><div class="metric-info"><h4>Active Operations</h4><h2>{{ ongoingEvents }}</h2></div></div>
      <div class="metric-card"><div class="metric-info"><h4>Inventory Stock</h4><h2>{{ availableResources }} / {{ totalResources }}</h2></div></div>
      <div class="metric-card"><div class="metric-info"><h4>Current Allocations</h4><h2>{{ totalAllocations }}</h2></div></div>
    </div>
  </div>
</div>

planner-dashboard.component.scss:
.dashboard-wrapper { padding: 40px; max-width: 1400px; margin: 0 auto; }
.hero-banner { border-radius: 20px; padding: 60px 50px; color: #fff; box-shadow: 0 20px 40px rgba(0,0,0,0.1); &.planner-theme { background: linear-gradient(135deg, #0F172A, #1E293B); } h1 { font-size: 2.5rem; margin: 0 0 10px 0; } }
.dashboard-content { margin-top: 40px; }
.metrics-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(260px, 1fr)); gap: 25px; }
.metric-card { background: #fff; border-radius: 16px; padding: 30px; border: 1px solid #e2e8f0; box-shadow: 0 10px 25px rgba(0,0,0,0.05); h4 { color: #64748b; margin: 0 0 10px 0; } h2 { color: #0F172A; font-size: 2.2rem; margin: 0; } &.highlight { background: #4F46E5; h4, h2 { color: #fff; } } }
.animate-slide-up { animation: slideUp 0.6s forwards; } @keyframes slideUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }

STEP 3: The Staff Dashboard
Create a new folder: client/src/app/staff-dashboard. Staff gets a unique, action-oriented landing page.
staff-dashboard.component.ts:
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-staff-dashboard',
  templateUrl: './staff-dashboard.component.html',
  styleUrls: ['./staff-dashboard.component.scss']
})
export class StaffDashboardComponent implements OnInit {
  username: string = '';
  
  ngOnInit(): void {
    this.username = localStorage.getItem('username') || 'Operations Team';
  }
}

staff-dashboard.component.html:
<div class="dashboard-wrapper">
  <header class="hero-banner staff-theme animate-slide-up">
    <div class="hero-content">
      <h1>Operations Hub</h1>
      <p class="subtitle">Welcome to the ground floor, {{ username | titlecase }}. Ready to execute?</p>
    </div>
  </header>

  <div class="quick-actions animate-slide-up">
    <h3>Staff Directives</h3>
    <div class="action-grid">
      <div class="action-card" routerLink="/view-events">
        <h4>Manage Event Operations</h4>
        <p>Update venue setup status and modify seat capacities instantly.</p>
        <button>Launch Operations</button>
      </div>
      <div class="action-card info-card">
        <h4>System Alerts</h4>
        <p>Keep an eye on your Orbital Beacon in the top right corner for incoming tasks from the Event Planner.</p>
      </div>
    </div>
  </div>
</div>

staff-dashboard.component.scss:
.dashboard-wrapper { padding: 40px; max-width: 1200px; margin: 0 auto; }
.hero-banner { border-radius: 20px; padding: 60px 50px; color: #fff; &.staff-theme { background: linear-gradient(135deg, #EA580C, #C2410C); } h1 { font-size: 2.5rem; margin: 0 0 10px 0; } }
.quick-actions { margin-top: 40px; h3 { color: #0F172A; font-size: 1.5rem; margin-bottom: 20px; } }
.action-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 25px; }
.action-card { background: #fff; padding: 30px; border-radius: 16px; border: 1px solid #e2e8f0; box-shadow: 0 10px 20px rgba(0,0,0,0.05); cursor: pointer; transition: transform 0.2s; &:hover { transform: translateY(-5px); border-color: #EA580C; } h4 { font-size: 1.2rem; color: #0F172A; } p { color: #64748b; line-height: 1.5; margin-bottom: 20px; } button { background: #EA580C; color: #fff; padding: 10px 20px; border: none; border-radius: 8px; font-weight: bold; cursor: pointer; } &.info-card { background: #FFF7ED; border-color: #FDBA74; &:hover { transform: none; cursor: default; } } }
.animate-slide-up { animation: slideUp 0.6s forwards; } @keyframes slideUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }

STEP 4: The Client Dashboard
Create a new folder: client/src/app/client-dashboard. Clients get a welcoming portal layout.
client-dashboard.component.ts:
import { Component, OnInit } from '@angular/core';
import { HttpService } from '../../services/http.service';

@Component({
  selector: 'app-client-dashboard',
  templateUrl: './client-dashboard.component.html',
  styleUrls: ['./client-dashboard.component.scss']
})
export class ClientDashboardComponent implements OnInit {
  username: string = '';
  activeEventsCount: number = 0;
  ownedTicketsCount: number = 0;

  constructor(private httpService: HttpService) {}

  ngOnInit(): void {
    this.username = localStorage.getItem('username') || 'Guest';
    
    // Check how many tickets they have in local storage
    const storedTickets = localStorage.getItem('myTickets_' + this.username);
    if (storedTickets) {
      this.ownedTicketsCount = JSON.parse(storedTickets).length;
    }

    // See how many events are available to book
    this.httpService.getActiveEvents().subscribe(data => {
      this.activeEventsCount = data.length;
    });
  }
}

client-dashboard.component.html:
<div class="dashboard-wrapper">
  <header class="hero-banner client-theme animate-slide-up">
    <div class="hero-content">
      <h1>Welcome, {{ username | titlecase }}!</h1>
      <p class="subtitle">Your premier portal for discovering and securing exclusive event access.</p>
    </div>
  </header>

  <div class="client-metrics animate-slide-up">
    <div class="metric-card" routerLink="/booking-details">
      <div class="card-left">
        <h4>Available Events</h4>
        <h2>{{ activeEventsCount }} Open</h2>
        <p>Click here to discover new events and secure your passes.</p>
      </div>
    </div>

    <div class="metric-card owned" routerLink="/booking-details">
      <div class="card-left">
        <h4>My Digital Wallet</h4>
        <h2>{{ ownedTicketsCount }} Secured Passes</h2>
        <p>View your QR codes or download your High-Res PDFs for entry.</p>
      </div>
    </div>
  </div>
</div>

client-dashboard.component.scss:
.dashboard-wrapper { padding: 40px; max-width: 1000px; margin: 0 auto; }
.hero-banner { border-radius: 20px; padding: 60px 50px; color: #fff; &.client-theme { background: linear-gradient(135deg, #0D9488, #0F766E); } h1 { font-size: 2.5rem; margin: 0 0 10px 0; } }
.client-metrics { display: grid; grid-template-columns: 1fr 1fr; gap: 30px; margin-top: 40px; }
.metric-card { background: #fff; border-radius: 16px; padding: 40px; border: 1px solid #e2e8f0; box-shadow: 0 10px 25px rgba(0,0,0,0.05); cursor: pointer; transition: transform 0.2s, box-shadow 0.2s; &:hover { transform: translateY(-5px); box-shadow: 0 15px 35px rgba(13, 148, 136, 0.15); border-color: #0D9488; } h4 { color: #64748b; font-size: 1.1rem; text-transform: uppercase; letter-spacing: 1px; margin: 0 0 10px 0; } h2 { font-size: 2.5rem; color: #0D9488; margin: 0 0 15px 0; } p { color: #475569; margin: 0; line-height: 1.5; } &.owned { &:hover { border-color: #4F46E5; box-shadow: 0 15px 35px rgba(79, 70, 229, 0.15); } h2 { color: #4F46E5; } } }
.animate-slide-up { animation: slideUp 0.6s forwards; } @keyframes slideUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }

Final Cleanup
You can now safely delete the old client/src/app/dashbaord folder. Your application is now modular, totally conflict-free, and enterprise-ready!
