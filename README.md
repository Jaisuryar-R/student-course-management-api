# Student Course Management API

A RESTful backend application for managing student records, courses, and student enrollments using Node.js, Express.js, and MySQL.

## Overview

The Student Course Management API provides endpoints for creating, retrieving, updating, and deleting student and enrollment records, as well as managing course information.

The documented functionality includes search, filtering, sorting, pagination, request validation, and error handling.

## Technology Stack

| Technology | Purpose |
|---|---|
| Node.js | JavaScript runtime |
| Express.js | Backend web framework |
| MySQL | Relational database |
| mysql2 | MySQL database connectivity |
| dotenv | Environment variable management |
| Postman | API testing |
| Git and GitHub | Version control and repository hosting |

## Features

### Student Management
- Create student records
- Retrieve all students
- Retrieve a student by ID
- Update student information
- Delete student records
- Search by name, email, or phone
- Sort and paginate student records

### Course Management
- Create courses
- Retrieve all courses
- Retrieve a course by ID
- Update course information
- Search by course name, code, or description
- Sort and paginate courses

### Enrollment Management
- Create student-course enrollments
- Retrieve all enrollments
- Retrieve an enrollment by ID
- Update enrollment information
- Delete enrollments
- Filter by student ID or course ID
- Sort and paginate enrollment records

### Data Validation and Error Handling
- Validate required fields
- Validate email addresses, phone numbers, and dates
- Handle duplicate student emails and course codes
- Validate student and course references
- Handle duplicate enrollments
- Return appropriate HTTP status codes for documented errors

## Project Structure

```text
student-course-management-api/
├── src/
│   ├── config/
│   │   └── db.js
│   ├── controllers/
│   │   ├── studentController.js
│   │   ├── courseController.js
│   │   └── enrollmentController.js
│   ├── routes/
│   │   ├── studentRoutes.js
│   │   ├── courseRoutes.js
│   │   └── enrollmentRoutes.js
│   └── app.js
├── .gitignore
├── package.json
├── package-lock.json
└── README.md
```

The `.env` file contains local configuration and should not be committed to a public repository.

## Architecture

The application follows a modular backend architecture.

```text
Client / Postman
       |
       v
 Express Server
       |
       v
     Routes
       |
       v
   Controllers
       |
       v
  MySQL Database
       |
       v
  JSON Response
```

- **Routes:** Define API endpoints and connect requests to controllers.
- **Controllers:** Process requests and execute application logic.
- **Database configuration:** Establishes connectivity to MySQL.
- **MySQL:** Stores student, course, and enrollment records.

## Database Design

Database name: `student_record_db`

The database documentation describes three main tables.

### 1. Students

| Field | Description |
|---|---|
| `student_id` | Primary key and unique student identifier |
| `name` | Student name |
| `email` | Unique email address |
| `phone` | Phone number |
| `date_of_birth` | Date of birth |
| `created_at` | Record creation timestamp |

### 2. Courses

| Field | Description |
|---|---|
| `course_id` | Primary key |
| `course_name` | Course name |
| `course_code` | Unique course code |
| `description` | Course description |
| `created_at` | Record creation timestamp |

### 3. Enrollments

| Field | Description |
|---|---|
| `enrollment_id` | Primary key |
| `student_id` | Reference to a student |
| `course_id` | Reference to a course |
| `enrollment_date` | Enrollment date |

The documented database design uses foreign keys to connect enrollments to students and courses. A unique constraint on the combination of `student_id` and `course_id` prevents duplicate enrollments.

### Relationships

- One student can have multiple enrollments.
- One course can have multiple enrollments.
- The enrollments table connects students and courses.

## API Documentation

### Base URL

```text
http://localhost:5000
```

The port and route prefixes should match the actual application configuration.

### Student Endpoints

| Method | Endpoint | Description |
|---|---|---|
| POST | `/students` | Create a student |
| GET | `/students` | Retrieve students |
| GET | `/students/:id` | Retrieve a student by ID |
| PUT | `/students/:id` | Update a student |
| DELETE | `/students/:id` | Delete a student |

#### Create a Student

`POST /students`

Example request body:

```json
{
  "name": "Test Student",
  "email": "teststudent@example.com",
  "phone": "9876543210",
  "date_of_birth": "2005-10-09"
}
```

Example response:

```json
{
  "message": "Student created successfully",
  "student_id": 2
}
```

### Course Endpoints

| Method | Endpoint | Description |
|---|---|---|
| POST | `/courses` | Create a course |
| GET | `/courses` | Retrieve courses |
| GET | `/courses/:id` | Retrieve a course by ID |
| PUT | `/courses/:id` | Update a course |

A course DELETE endpoint is not documented as implemented in the original project.

#### Create a Course

`POST /courses`

Example request body:

```json
{
  "course_name": "Advanced Java Programming",
  "course_code": "JAVA201",
  "description": "Advanced Java programming course"
}
```

### Enrollment Endpoints

| Method | Endpoint | Description |
|---|---|---|
| POST | `/enrollments` | Create an enrollment |
| GET | `/enrollments` | Retrieve enrollments |
| GET | `/enrollments/:id` | Retrieve an enrollment by ID |
| PUT | `/enrollments/:id` | Update an enrollment |
| DELETE | `/enrollments/:id` | Delete an enrollment |

#### Create an Enrollment

`POST /enrollments`

Example request body:

```json
{
  "student_id": 2,
  "course_id": 1,
  "enrollment_date": "2026-10-01"
}
```

Create the student and course records before creating an enrollment that references them.

## Search, Filtering, Sorting and Pagination

The existing documentation describes the following query parameters.

| Resource | Parameters |
|---|---|
| Students | `search`, `sort`, `order`, `page`, `limit` |
| Courses | `search`, `sort`, `order`, `page`, `limit` |
| Enrollments | `student_id`, `course_id`, `sort`, `order`, `page`, `limit` |

### Examples

Search students:

```http
GET /students?search=Test
```

Sort students by name:

```http
GET /students?sort=name&order=asc
```

Retrieve a page of students:

```http
GET /students?page=1&limit=5
```

Search and paginate courses:

```http
GET /courses?search=Java&page=1&limit=5&sort=course_name&order=asc
```

Filter and sort enrollments:

```http
GET /enrollments?student_id=2&sort=enrollment_date&order=desc&page=1&limit=5
```

Pagination uses a page number and a result limit. The documented response structure can include the current page, result limit, total records, total pages, and returned data.

## Installation and Setup

### Prerequisites

Install the following tools:

- Node.js and npm
- MySQL Server
- Git
- Postman (optional, for API testing)

### 1. Clone Your Repository

After uploading this project to your own GitHub repository, use its URL:

```bash
git clone https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.git
cd YOUR-REPOSITORY
```

Replace the placeholders with your actual repository details.

### 2. Install Dependencies

```bash
npm install
```

### 3. Configure MySQL

Create the database:

```sql
CREATE DATABASE student_record_db;
```

Select the database:

```sql
USE student_record_db;
```

Create the required tables using the SQL definitions in the database documentation or your database setup script.

### 4. Configure Environment Variables

Create a local `.env` file in the project root if the application expects these variables:

```env
DB_HOST=localhost
DB_USER=root
DB_PASSWORD=YOUR_MYSQL_PASSWORD
DB_NAME=student_record_db
DB_PORT=3306
PORT=5000
```

Replace the example values with your local MySQL configuration.

**Security:** Never publish your real database password, API keys, or other secrets. Ensure `.env` is excluded from Git.

### 5. Start the Application

The original project documentation specifies this command:

```bash
node src/app.js
```

Use the command above unless you have separately verified another start script in `package.json`.

### 6. Test the API

Open Postman and send requests to the documented endpoints.

For example:

```http
GET http://localhost:5000/students
```

Confirm that the server is running, the database connection succeeds, and the response matches the expected API behavior.

## HTTP Status Codes

The original documentation describes these status codes:

| Status | Meaning |
|---|---|
| `200 OK` | Request completed successfully |
| `201 Created` | Resource created successfully |
| `400 Bad Request` | Invalid request data |
| `404 Not Found` | Resource not found |
| `409 Conflict` | Duplicate or conflicting data |
| `500 Internal Server Error` | Server or database error |

Actual status codes depend on the implemented endpoint and error handling.

## Security Considerations

The original project documentation describes parameterized MySQL queries, which help protect against SQL injection when used correctly.

Additional recommendations:

- Keep credentials in environment variables.
- Exclude `.env` and `node_modules` from Git.
- Validate and sanitize incoming request data.
- Avoid exposing internal database errors to API clients.
- Add authentication and authorization before exposing sensitive student data publicly.

## Learning Outcomes

This project provides an opportunity to learn about:

- REST API design
- Node.js and Express.js
- MySQL database connectivity
- Relational database design
- CRUD operations
- SQL queries and parameterized queries
- Request validation and error handling
- Search, filtering, sorting, and pagination
- Environment variables
- Modular backend architecture
- API testing with Postman
- Git and GitHub

## Future Improvements

Potential enhancements include:

- Authentication and authorization
- Role-based access control
- Course deletion endpoint
- Swagger/OpenAPI documentation
- Automated API tests
- Advanced validation
- Student and course reports
- Dashboard integration
- Cloud deployment
- Docker support

## Credits and Project Attribution

This repository contains a Student Course Management API based on an existing project developed as part of the CodSoft Backend Development Internship.

**Repository Maintainer: Jaisurya R

**GitHub:** [Jaisuryar-R](https://github.com/Jaisuryar-R)

**Original Repository:(https://github.com/Jaisuryar-R/student-course-management-api.git)

**Original Project:** `Task1-Student-Record-API`

The repository setup and README documentation have been updated for this GitHub publication. The original implementation is credited to its original author.

Further modifications and features will be documented according to the contributions made.

## Conclusion

The Student Course Management API demonstrates a modular backend architecture for managing students, courses, and enrollments using Node.js, Express.js, and MySQL.

The project documentation describes CRUD operations, relational database management, search, filtering, sorting, pagination, request validation, and error handling.
