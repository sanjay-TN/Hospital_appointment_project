# Hospital Appointment Project

Deployed app: `https://hospital-appointment-project-1.onrender.com`

A full-stack hospital appointment management system built to simplify patient booking, doctor scheduling, and appointment queue handling. The project includes a Spring Boot backend with JWT-based authentication, a PostgreSQL database, and a lightweight HTML/CSS/JavaScript frontend.

## Overview

This application supports three main user roles:

- `ADMIN` can create, update, view, and delete doctor profiles.
- `DOCTOR` can create schedules, manage appointment slots, view queue details, and update consultation status.
- `PATIENT` can register, log in, book appointments, view appointment history, cancel bookings, and check live queue status.

Live project links:

- `Live Demo`: `https://hospital-appointment-project-1.onrender.com`
- `Live API`: `https://hospital-appointment-project.onrender.com`

## Features

- Role-based authentication and authorization using JWT
- Patient registration and login
- Admin doctor management
- Doctor schedule creation and updates
- Appointment booking with queue number generation
- Queue tracking for both doctor and patient views
- Appointment lifecycle management: `BOOKED`, `IN_PROGRESS`, `COMPLETED`, `CANCELLED`
- Notification records stored when appointments are booked
- Docker support for PostgreSQL, backend, and frontend services

## Tech Stack

- `Frontend`: HTML, CSS, JavaScript, Nginx
- `Backend`: Java 17, Spring Boot, Spring Security, Spring Data JPA
- `Database`: PostgreSQL
- `Authentication`: JWT
- `Containerization`: Docker, Docker Compose

## Project Structure

```text
Hospital_appointment_project/
|-- Hospital_appointment-backend/
|   |-- src/main/java/com/appointment/
|   |   |-- config/
|   |   |-- controllers/
|   |   |-- dtos/
|   |   |-- entities/
|   |   |-- enums/
|   |   |-- repositories/
|   |   |-- security/
|   |   `-- service/
|   `-- src/main/resources/
|       `-- application.properties
|-- Hospital_appointment_frontend/
|   |-- css/
|   |-- js/
|   |-- index.html
|   |-- register.html
|   |-- admin.html
|   |-- doctor.html
|   `-- patient.html
|-- docker-compose.yml
`-- README.md
```

## Main Modules

### Authentication

- `POST /auth/register` registers a new user
- `POST /auth/login` returns a JWT token after successful login

### Admin

- Create doctor profiles
- View all doctors
- Update doctor specialization, experience, and consultation fee
- Delete doctors

### Doctor

- Create schedules with date, start time, end time, and max appointments
- View own schedules
- Update or delete schedules
- View appointment queue for a selected schedule
- Start and complete consultations

### Patient

- Book appointments using doctor ID and schedule ID
- View paginated appointment history
- Cancel appointments
- Check queue number, patients ahead, and currently serving status

## Local Setup

### Prerequisites

- Java 17
- Maven
- PostgreSQL
- Docker and Docker Compose (optional)

### Backend Setup

1. Open the backend folder:

```bash
cd Hospital_appointment-backend
```

2. Start PostgreSQL and create a database named `Hospital_appointment`, or update the datasource values in `application.properties`.

3. Run the backend:

```bash
mvn spring-boot:run
```

4. The API will start on:

```text
http://localhost:8080
```

### Frontend Setup

The frontend is a static HTML/CSS/JS app. Open the frontend folder and serve it with any static server, or open the HTML files directly in a browser.

Important:

- `Hospital_appointment_frontend/js/app.js` currently uses `https://hospital-appointment-project.onrender.com` as `BASE_URL`.
- If you want the frontend to talk to your local backend, change `BASE_URL` to `http://localhost:8080` before running it locally.

## Docker Setup

Create a root `.env` file with values similar to:

```env
POSTGRES_DB=Hospital_appointment
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
JWT_SECRET=your_jwt_secret_key_here
```

Then run:

```bash
docker compose up --build
```

Services:

- Frontend: `http://localhost:8081`
- Backend: `http://localhost:8080`
- PostgreSQL: `localhost:5432`

Note:

- The frontend Docker image serves static files only.
- Because `BASE_URL` is hardcoded in `Hospital_appointment_frontend/js/app.js`, update it before building if you want the Dockerized frontend to call the local backend instead of the deployed API.

## Database Notes

The backend uses JPA with:

- `spring.jpa.hibernate.ddl-auto=update`
- automatic table creation/update on startup

Main entities include:

- `User`
- `Doctor`
- `DoctorSchedule`
- `Appointment`
- `Notification`

## Future Improvements

- Add a deployed frontend link and screenshots
- Replace hardcoded frontend API URL with environment-based configuration
- Add Swagger or API documentation
- Add unit and integration tests for major flows
- Improve reminder scheduling to avoid duplicate repeated notifications

## Author

Created as a full-stack hospital appointment booking and queue management project for learning and portfolio use.
