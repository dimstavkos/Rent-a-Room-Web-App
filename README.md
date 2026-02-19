# Rent-a-House - A Full-Stack Web Application for Property Rentals


## Overview

This project was developed as part of a university course with a focus on applying practical software engineering principles. It implements a full-stack web application for property rentals, inspired by modern accommodation platforms. The system enables users to act as hosts or renters, supporting property management, booking workflows, secure authentication, messaging, and personalized recommendations.

The application is structured as a three-tier system:

- A relational database for data persistence
- A RESTful backend API handling business logic and security
- A frontend application for user interaction

Special emphasis was placed on database schema design, layered backend architecture, role-based authorization, and controlled API data exposure.

The platform supports three user roles: administrator, host, and renter, each with clearly defined permissions.



### Technologies Used

| Layer | Technologies |
| --- | --- |
| Backend | FastAPI, MySQL, SQLAlchemy |
| Frontend | Vue.js 3, Pinia |
| Auth & Security | JWT |
| Recommendation System | Matrix Factorization |


### Key Features

- **Property Management:** Search, filter, and manage properties with booking workflows.
- **User Features:** Role-based access control, JWT authentication, messaging system, and personalized recommendations.



## Database Design
The relational schema was designed in MySQL Workbench and implemented in MySQL. The database schema (shown below) covers core entities such as Users, Properties, Bookings, Ratings, Messages, and Property Views.


  <img src="docs/images/Database.png" width="75%" />


Role-based access control is enforced at the application level. Referential integrity is maintained through primary and foreign keys, and normalization principles were applied to minimize redundancy. Strategic indexing supports efficient query execution.

Database interaction is handled through SQLAlchemy ORM, mapping relational tables to Python classes and enabling structured query generation.

## Backend Implementation
The backend was implemented using FastAPI and follows a layered architectural approach to ensure separation of concerns.

The main layers include:

- Routing layer (HTTP request handling)
- Controller layer (business logic)
- Model layer (database interaction via SQLAlchemy)

Pydantic schemas are used to validate and serialize responses, preventing uncontrolled exposure of database objects.

The API supports CRUD operations, property search, booking management, messaging, and administrative data export.

## Authentication and Authorization
Authentication is implemented using JSON Web Tokens (JWT). Upon successful login, a token is generated and returned to the user. This token must be included in subsequent requests to protected endpoints.

Each protected request undergoes token validation to verify authenticity and expiration. Unauthorized access results in an HTTP 401 response. In addition to authentication, role-based authorization is enforced to restrict access depending on whether the user acts as an administrator, host, or renter.

This mechanism ensures that sensitive operations, such as user management or data export, are accessible only to authorized roles.


  <img src="docs/images/Login.png" width="75%" />


## Frontend Implementation

The frontend was developed using Vue.js 3 with the Composition API. State management is handled using Pinia to centralize authentication state and user data. The UI structure was based on an open-source template and adapted to support the application’s functional requirements.

The interface adapts dynamically based on user roles:

- Hosts can manage property listings and review booking requests.
- Renters can search properties, submit booking requests, and manage reservations.
- Administrators have extended management capabilities.

   
  <img src="docs/images/ManageProperties.png" width="45%" />   <img src="docs/images/Search.png" width="45%" />   
The frontend communicates exclusively with the backend through structured API calls, maintaining a clean separation between presentation and business logic.

## Recommendation System
The platform incorporates a personalized recommendation system based on collaborative filtering using matrix factorization.

A sparse user–property rating matrix is constructed from explicit ratings. Matrix factorization is applied to approximate missing values and generate predicted preferences for unseen properties.

Model parameters are optimized using gradient descent to minimize reconstruction error. Additionally, implicit feedback (property view frequency) is incorporated to enhance personalization.

This component integrates concepts from linear algebra and numerical optimization into the backend workflow.


 <img src="docs/images/Recomendations.png" width="75%" />

## Running the Application

### 1. Database Setup

- Create a MySQL database.
- Use the provided database model (database/model_rentahouse.mwb) to generate the schema via MySQL Workbench or manually create the tables based on the schema design.
- Update database credentials in `backend/.env`.
- Seed the database with initial data.

```
cd backend
python seeder.py
```
This script populates the database with sample users, properties, bookings, and ratings required for testing the application.

### Backend

```
cd backend
pip install -r requirements.txt
uvicorn main:app --reload
```

The backend API runs locally at: `http://127.0.0.1:8000`


### Frontend
```
cd frontend
npm install
npm run dev
```
The frontend runs locally and communicates with the backend API.
