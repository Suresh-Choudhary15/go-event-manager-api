# Go Event Manager API

A lightweight REST API for managing events, user accounts, and event registrations. Built with Go, Gin, and SQLite.

## Features

- User signup and login
- JWT-based authentication
- Create, read, update, and delete events
- Register and unregister users for events
- SQLite database persistence
- API test files included for quick manual testing

## Tech Stack

- Go
- Gin Web Framework
- SQLite
- JWT Authentication
- bcrypt-style password hashing

## Project Structure

```text
.
├── api-test/            # HTTP request samples for testing endpoints
├── db/                  # Database initialization and schema setup
├── middlewares/         # Auth middleware
├── models/              # User and Event data models
├── routes/              # Route registration and handlers
├── utils/               # JWT and password utility helpers
├── go.mod               # Go module definition
├── main.go              # Application entry point
├── api.db               # SQLite database file (generated at runtime)
└── README.md            # Project documentation
```

## Getting Started

### Prerequisites

- Go 1.22 or newer
- Git

### Install dependencies

```bash
go mod tidy
```

### Run the application

```bash
go run .
```

The server starts on:

```text
http://localhost:8080
```

## API Endpoints

### Public routes

- `POST /signup` - Create a new user account
- `POST /login` - Log in and receive a JWT token
- `GET /events` - Get all events
- `GET /events/:id` - Get a single event by ID

### Protected routes

All routes below require a valid JWT token in the `Authorization` header.

```http
Authorization: Bearer <your_token>
```

- `POST /events` - Create an event
- `PUT /events/:id` - Update an event
- `DELETE /events/:id` - Delete an event
- `POST /events/:id/register` - Register for an event
- `DELETE /events/:id/register` - Cancel event registration

## Example Requests

### Sign up

```bash
curl -X POST http://localhost:8080/signup \
  -H "Content-Type: application/json" \
  -d '{
    "email": "user@example.com",
    "password": "secret123"
  }'
```

### Log in

```bash
curl -X POST http://localhost:8080/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "user@example.com",
    "password": "secret123"
  }'
```

### Create an event

```bash
curl -X POST http://localhost:8080/events \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer <token>" \
  -d '{
    "name": "Tech Meetup",
    "description": "A local developer meetup",
    "location": "Lagos",
    "dateTime": "2026-10-10T18:00:00Z"
  }'
```

## Testing with HTTP Files

The project includes sample API requests in the `api-test/` folder. These files can be used with VS Code REST Client or similar tools.

## Notes

This project is a simple backend API for learning and practicing Go, REST API design, JWT authentication, and SQLite integration.
