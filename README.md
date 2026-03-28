🎫 TICKETING SYSTEM API
📌 OVERVIEW

The Ticketing System is a role-based backend application built using ASP.NET Core Web API. It helps teams manage tickets, assign tasks, and generate reports efficiently.

🚀 FEATURES
🔐 JWT Authentication & Authorization
👥 Role-Based Access Control (Admin, PM, TL, Dev, QA)
🎫 Ticket Management (Create, Assign, Update)
📊 Excel Report Generation (ClosedXML)
🧾 Clean Architecture (Layered Structure)
⚡ Async/Await Implementation
🏗️ PROJECT STRUCTURE
TicketingSystem
│
├── TicketingSystem.API            # Controllers (Presentation Layer)
├── TicketingSystem.Application    # Services, DTOs (Business Logic)
├── TicketingSystem.Domain         # Entities, Enums
├── TicketingSystem.Infrastructure # DB Context, Repositories
🔐 AUTHENTICATION & AUTHORIZATION
Uses JWT Token for secure authentication

Role-based access using:

[Authorize(Roles = "...")]
👥 ROLES
Admin
ProjectManager
TeamLead
Developer
QA
🔄 TICKET WORKFLOW

Created → Assigned → In Progress → Resolved → Closed

📡 API ENDPOINTS
🔐 AUTH APIs
Method	Endpoint	Access
POST	/api/auth/register	Public
POST	/api/auth/login	Public
🎫 TICKET APIs
Method	Endpoint	Access	Role
POST	/api/tickets	Admin, PM	Admin, PM
GET	/api/tickets	Admin, PM, TL	Admin, PM, TL
GET	/api/tickets/{id}	All (based access)	All
PUT	/api/tickets/{id}	Admin, PM, TL	Admin, PM, TL
🔄 WORKFLOW APIs
Method	Endpoint	Access	Role
PUT	/api/tickets/{id}/assign	Admin, PM, TL	Admin, PM, TL
PUT	/api/tickets/{id}/status	All	All Roles
📊 REPORT API
Method	Endpoint	Access	Role
GET	/api/reports/export	Admin, PM	Admin, PM
🗄️ DATABASE SCHEMA (SIMPLIFIED)
👤 USERS
Id (Guid)
Email
Password
Role
🎫 TICKETS
Id (Guid)
Title
Description
Status (Enum)
Priority (Enum)
AssignedToUserId (Guid)
CreatedBy (Guid)
CreatedDate (DateTime)
⚙️ CONFIGURATION

Update appsettings.json:

{
  "ConnectionStrings": {
    "DefaultConnection": "your_connection_string"
  },
  "Jwt": {
    "Key": "your_secret_key",
    "Issuer": "your_issuer",
    "Audience": "your_audience"
  },
  "Email": {
    "Smtp": "smtp.gmail.com",
    "User": "your_email",
    "Password": "your_app_password"
  }
}
🔥 PRO TIP (VERY IMPORTANT)

Before pushing code to GitHub:

❌ Do NOT commit real passwords
✅ Always use placeholders like:

"your_secret_key"
"your_email"
"your_app_password"

👉 For real credentials, use:

User Secrets (local)
Environment Variables (production)
▶️ HOW TO RUN
# Clone repository

# Navigate to project
cd TicketingSystem

# Apply migrations
dotnet ef migrations add InitialCreate
dotnet ef database update

# Run project
dotnet run
📊 REPORT FEATURE
Export tickets to Excel
Built using ClosedXML
Includes:
Ticket details
Status
Priority
Dates
