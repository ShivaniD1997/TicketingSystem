🎫 Ticketing System API
📌 Overview
The Ticketing System is a role-based backend application built using ASP.NET Core Web API. It helps teams manage tickets, assign tasks and generate reports efficiently.

🚀 Features
🔐 JWT Authentication & Authorization

👥 Role-Based Access Control (Admin, PM, TL, Dev, QA)

🎫 Ticket Management (Create, Assign, Update)

📊 Excel Report Generation (ClosedXML)

🧾 Clean Architecture (Layered Structure)

⚡ Async/Await Implementation

🏗️ Project Structure
TicketingSystem
│
├── TicketingSystem.API            # Controllers (Presentation Layer)
├── TicketingSystem.Application    # Services, DTOs (Business Logic)
├── TicketingSystem.Domain         # Entities, Enums
├── TicketingSystem.Infrastructure # DB Context, Repositories
🔐 Authentication & Authorization
Uses JWT Token for secure authentication

Role-based access using [Authorize(Roles = "...")]

👥 Roles
Admin

ProjectManager

TeamLead

Developer

QA

🔄 Ticket Workflow
Created → Assigned → In Progress → Resolved → Closed
📡 API Endpoints
🔐 Auth APIs
Method	Endpoint	Access
POST	/api/auth/register	Public
POST	/api/auth/login	Public

🎫 Ticket APIs
Method	Endpoint	Access     Role
POST	/api/tickets	Admin, PM
GET	/api/tickets	Admin, PM, TL
GET	/api/tickets/{id}	All (based on access)
PUT	/api/tickets/{id}	Admin, PM, TL

🔄 Workflow APIs
Method	Endpoint	Access                        Role
PUT	/api/tickets/{id}/assign	Admin, PM, TL
PUT	/api/tickets/{id}/status	All Roles

📊 Report API
Method	Endpoint	Access     Role
GET	/api/reports/export	Admin, PM
🗄️ Database Schema (Simplified)
👤 Users
Id (Guid)

Email

Password

Role

🎫 Tickets
Id (Guid)

Title

Description

Status (Enum)

Priority (Enum)

AssignedToUserId (Guid)

CreatedBy (Guid)

CreatedDate (DateTime)

⚙️ Configuration
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

▶️ How to Run
# Clone repository

# Navigate to project
cd TicketingSystem

# Apply migrations
dotnet ef migrations add InitialCreate
dotnet ef database update

# Run project
dotnet run

📊 Report Feature
Export tickets to Excel

Built using ClosedXML

Includes ticket details, status, priority, and dates























