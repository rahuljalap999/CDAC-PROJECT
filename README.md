# 🏥 Arogyam – Hospital Management System

Arogyam is a Full Stack Hospital Management System developed as a CDAC project using Spring Boot (Backend), React.js (Frontend), MySQL (Database), and JWT Authentication.

The system manages hospital operations including Employees, Patients, OPDs, and Prescriptions with secure role-based access control.

# 🚀 Tech Stack

## Backend
- Java
- Spring Boot
- Spring Security
- JWT Authentication
- Spring Data JPA
- Hibernate
- MySQL
- Maven

## Frontend
- React.js
- React Router
- Axios
- Bootstrap

# 🏗️ Architecture

React Frontend (Port 3000)
        ↓
Spring Boot REST APIs (Port 8081)
        ↓
MySQL Database

# 🔐 Authentication Flow:
User → Login 
     → JWT Token Generated 
     → Stored in localStorage 
     → Sent in Authorization Header 
     → Validated by JwtFilter


# 🔐 Authentication & Security

- JWT-based authentication
- Token expiry: 5 hours
- Stateless session management
- Custom JwtFilter (OncePerRequestFilter)
- Role-Based Access Control
- Password encryption using BCrypt
- Global Exception Handling

JWT token contains:
- username
- role
- id (Employee ID or Patient ID)

Token is:
- Stored in localStorage
- Attached to every request via Axios interceptor
- Validated in Spring Security filter chain

# 👥 User Roles

The system supports 4 roles:

1. Administrator
2. Doctor
3. Receptionist
4. Patient

Each role has restricted access based on Spring Security configuration.

# 🧑‍💼 Administrator Module

## Features
- Add Employee
- Update Employee
- Activate / Deactivate Employee
- Delete Employee
- View All Employees
- View Pending OPDs
- View Dashboard Statistics

## APIs
- POST /api/admin/employees
- PUT /api/admin/employees
- GET /api/admin/employees
- PATCH /api/admin/employees/{eid}/status/{status}
- DELETE /api/admin/employees/{eid}
- GET /api/dashboard/stats
- GET /api/admin/employees/doctors

# 👨‍⚕️ Doctor Module

## Features
- View OPD Queue
- Add Prescription
- Update Prescription
- View Patient History
- View Own Patient Prescription History

## APIs
- GET /api/doctor/queue/{doctorId}
- GET /api/doctor/history/{pid}
- POST /api/doctor/prescription/{opdid}
- PUT /api/doctor/prescription
- GET /api/doctor/patient/history/{pid}


Doctor sees:
- OPD ID
- Visit Date
- Patient ID
- Status (Pending / Done)

# 🧑‍💻 Receptionist Module

## Features
- Register Patient
- Update Patient
- Delete Patient
- Assign Doctor to Patient
- Create OPD
- Manage OPDs
- View Patients by Doctor

## APIs
- POST /api/receptionist/patients
- PUT /api/receptionist/patients
- GET /api/receptionist/patients
- GET /api/receptionist/patients/{pid}
- GET /api/receptionist/patients/doctor/{doctorId}
- DELETE /api/receptionist/patients/{pid}

- POST /api/opd
- GET /api/opd/pending
- PATCH /api/opd/{opdid}/status/{status}
- DELETE /api/opd/{opdid}

# 🧑 Patient Module

## Features
- Login using Patient ID
- View Own Prescription History

## APIs
- GET /api/doctor/patient/history/{pid}

Patients can only access their own data.

# 📊 Dashboard

Accessible by:
- Administrator
- Doctor
- Receptionist

Displays:
- Total Active Doctors
- Total Patients
- Total Employees
- Total Income (sum of OPD fees)

## APIs
- GET /api/dashboard/stats


# 🏗️ Database Design

## Employee
- One-to-One → Login
- One-to-Many → Patients
- One-to-Many → OPDs

## Patient
- Many-to-One → Doctor
- One-to-Many → OPDs

## OPD
- Many-to-One → Patient
- Many-to-One → Doctor
- One-to-One → OPDDetails

## OPDDetails
Contains:
- Symptoms
- Diagnosis
- Medicines & Dose
- Dos / Don'ts
- Investigations
- Follow-up Date
- Fees


# ⚙️ How to Run the Project

## 1️⃣ Backend Setup

```
cd arogyam-backend
mvn clean install
mvn spring-boot:run
```

Update `application.properties`:

```
spring.datasource.url=jdbc:mysql://localhost:3306/arogyam
spring.datasource.username=root
spring.datasource.password=yourpassword
spring.jpa.hibernate.ddl-auto=update
server.port=8081
```

Backend runs at: http://localhost:8081

## 2️⃣ Frontend Setup

```
cd arogyam-frontend
npm install
npm start
```

Frontend runs at: http://localhost:3000

# 🧠 Key Concepts Implemented

- JWT Authentication
- Custom Security Filter
- Role-Based Authorization
- DTO Pattern
- JPA Entity Relationships
- Validation Annotations
- Global Exception Handling
- Axios Interceptors
- React Protected Routes
- Stateless Security Configuration


# ❗ Challenges Faced

- Handling 403 Forbidden errors
- Correct Spring Security role mapping
- CORS configuration between frontend and backend
- Preventing self-deletion of logged-in admin
- Managing OPD–Prescription one-to-one mapping
- Token expiration handling
- Validation for Employee ID (EMP*) and Patient ID (P*)


# 🔮 Future Enhancements

- AWS Deployment
- Dockerization
- Email Notifications
- Payment Integration
- Appointment Scheduling System











