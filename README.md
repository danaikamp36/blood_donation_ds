# Blood Donation Management System

## ---------------------Description---------------------
This project is a web-based Blood Donation Management System, built using Spring Boot (backend) and Vue.js (frontend). It enables users to register as blood donors, manage donation requests, and handle administrative tasks related to blood donations. The system ensures role-based access using Spring Security and supports different user roles, including Admin, Secretary, User, and Blood Donor.


## -------------------Tech_Stack------------------------
->  Backend: Spring Boot, Spring Security, Spring Data JPA,PostgreSQL

->  Frontend: Vue.js

->  Database: PostgreSQL (Docker containerized)

->  Authentication & Authorization: Spring Security (Role-based access control)


## --------------------Features--------------------------
### Citizen (Blood Donor)

  -Apply to become a blood donor (Profile creation)

  -Update contact information
    
  -Modify personal details
    
  -Select available blood donation events (Based on location & last donation date)

### -Admin

  -Create user accounts and assign roles

  -Modify user details

  -Delete users from the system

### -Secretary
  
  -Review blood donor applications (Approve/Reject)
  
  -Create and manage blood donation events


## ----------------Deployment & Setup----------------
### -Prerequisites
    
  -Java & Maven
    
  -Docker
    
  -Node.js & npm
    
  -IntelliJ IDEA (or another IDE for Java development)


## -----------------Run the Project---------------------
1.Set up PostgreSQL Database using Docker:
  ```bash
  docker run --name ds-lab-pg --rm \
  -e POSTGRES_PASSWORD=pass123 \
  -e POSTGRES_USER=dbuser \
  -e POSTGRES_DB=aimodosia \
  -d -p 5432:5432 -v ds-lab-vol:/var/lib/postgresql/data \
  postgres:14
  ```

2.Start the Backend:
  Navigate to the backend folder and run DemoApplication.java

3.Start the Frontend:
  Navigate to the frontend folder and run:
  ```bash
    npm install
    npm run dev
  ```

4.Access the Application:
  The frontend should be available at: https://localhost:5173/


## ---------------------Notes----------------------------
The frontend communicates only with the backend REST API (no direct database access).

Role-based access control ensures users can only perform actions allowed by their role.
