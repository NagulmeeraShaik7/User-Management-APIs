# User Management API

A robust and efficient Flask-based API for managing user accounts, including authentication, CRUD operations, and user search functionality. This project demonstrates best practices in API development, including clear architecture (controllers, use cases, repositories), robust error handling, JWT-based authentication, and Swagger UI for API documentation.

## Table of Contents

- [Features](#features)
- [Project Structure](#project-structure)
- [Technologies Used](#technologies-used)
- [Setup and Installation](#setup-and-installation)
  - [Prerequisites](#prerequisites)
  - [Environment Variables](#environment-variables)
  - [Installation Steps](#installation-steps)
- [Database](#database)
- [API Endpoints](#api-endpoints)
  - [Authentication](#authentication)
  - [Users](#users)
- [Error Handling](#error-handling)
- [API Documentation (Swagger UI)](#api-documentation-swagger-ui)
- [Postman Collection](#postman-collection)
- [Contributing](#contributing)
- [License](#license)

## Features

* **User Authentication:** Secure login with JWT (JSON Web Tokens).
* **User Management (CRUD):** Create, Read, Update, and Delete user records.
* **User Search:** Search users by name.
* **Robust Error Handling:** Consistent and informative error responses with appropriate HTTP status codes.
* **Input Validation:** Server-side validation for user input.
* **Password Hashing:** Secure storage of passwords using `Werkzeug`'s hashing functions.
* **Swagger UI Integration:** Interactive API documentation for easy testing and exploration.
* **Clear Architecture:** Separation of concerns using Controllers, Use Cases, and Repositories.
* **Environment Variable Configuration:** Secure handling of sensitive information.

## Project Structure

The project follows a modular and layered architecture: 



# User Management API

A robust and efficient Flask-based API for managing user accounts, including authentication, CRUD operations, and user search functionality. This project demonstrates best practices in API development, including clear architecture (controllers, use cases, repositories), robust error handling, JWT-based authentication, and Swagger UI for API documentation.

## Table of Contents

- [Features](#features)
- [Project Structure](#project-structure)
- [Technologies Used](#technologies-used)
- [Setup and Installation](#setup-and-installation)
  - [Prerequisites](#prerequisites)
  - [Environment Variables](#environment-variables)
  - [Installation Steps](#installation-steps)
- [Database](#database)
- [API Endpoints](#api-endpoints)
  - [Authentication](#authentication)
  - [Users](#users)
- [Error Handling](#error-handling)
- [API Documentation (Swagger UI)](#api-documentation-swagger-ui)
- [Postman Collection](#postman-collection)
- [Contributing](#contributing)
- [License](#license)

## Features

* **User Authentication:** Secure login with JWT (JSON Web Tokens).
* **User Management (CRUD):** Create, Read, Update, and Delete user records.
* **User Search:** Search users by name.
* **Robust Error Handling:** Consistent and informative error responses with appropriate HTTP status codes.
* **Input Validation:** Server-side validation for user input.
* **Password Hashing:** Secure storage of passwords using `Werkzeug`'s hashing functions.
* **Swagger UI Integration:** Interactive API documentation for easy testing and exploration.
* **Clear Architecture:** Separation of concerns using Controllers, Use Cases, and Repositories.
* **Environment Variable Configuration:** Secure handling of sensitive information.

## Project Structure

The project follows a modular and layered architecture:
```
messy-migration/
├── .env                  # Environment variables (e.g., secret keys)
├── app.py                # Main Flask application entry point
├── init_db.py            # Script to initialize the SQLite database with sample data
├── requirements.txt      # Python dependencies
└── src/
├── apps/
│   ├── controllers/      # Handles HTTP requests, calls use cases, returns responses
│   │   └── user_controller.py
│   ├── models/           # Data models (e.g., User class)
│   │   └── user_model.py
│   ├── repositories/     # Handles database interactions (CRUD operations)
│   │   └── user_repository.py
│   ├── routes/           # Defines API endpoints and maps them to controllers
│   │   └── user_route.py
│   ├── usecases/         # Contains business logic, interacts with repositories
│   │   └── user_usecase.py
│   └── utils/            # Utility functions (e.g., input validators)
│       └── validators.py
├── middlewares/          # Custom Flask middleware (e.g., authentication, error handling)
│   ├── auth_middleware.py
│   └── error_middleware.py
└── swagger_config.py     # OpenAPI (Swagger) specification definition

``` 


## Technologies Used

* **Python 3.x**
* **Flask:** Web framework
* **SQLite:** Database (for simplicity in this example)
* **PyJWT:** For JSON Web Token (JWT) implementation
* **Werkzeug:** For password hashing (`generate_password_hash`, `check_password_hash`)
* **python-dotenv:** For loading environment variables
* **Flask-Swagger-UI:** To serve interactive API documentation

## Setup and Installation

### Prerequisites

* Python 3.8+ (recommended)
* `pip` (Python package installer)

### Environment Variables

Create a `.env` file in the root directory of your project (`messy-migration/`) and add the following:

```env
SECRET_KEY=your_flask_session_secret_key_here_generate_a_strong_one
JWT_SECRET_KEY=your_jwt_signing_secret_key_here_generate_a_strong_one
DATABASE_URL=sqlite:///users.db
```

- Install Dependencies
``` 
pip install -r requirements.txt
```

- Inititialize the database

```
python init_db.py
```

- Run the application 

```
python app.py
```

- Access the Swagger UI at `http://localhost:5000/swagger` 

# Error Handling 

  The API provides clear and consistent error responses in JSON format. Common error types include: 

  - `400 Bad Request`: Returned when the request is invalid or cannot be processed. This includes errors such as missing 

  - `401 Unauthorized`: Returned when the user is not authenticated or does not have the necessary permissions. 

  - `404 Not found`: Resource not found.
  - `405 Method Not Allowed`: The method is not allowed for the requested resource.
  - `500 Internal Server Error`: Returned when an unexpected error occurs on the server. This can be due to a variety of reasons such as database errors, server overload, or other internal issues. 


  ## API Endpoints

All API endpoints are accessible via `http://127.0.0.1:5000`. For interactive documentation and testing, please refer to the [API Documentation (Swagger UI)](#api-documentation-swagger-ui) section.

### Authentication

| Method | Path         | Description                 | Authentication |
| :----- | :----------- | :-------------------------- | :------------- |
| `POST` | `/login`     | Authenticate user, get JWT  | None           |

### Users

| Method   | Path                  | Description                                 | Authentication |
| :------- | :-------------------- | :------------------------------------------ | :------------- |
| `POST`   | `/users`              | Create a new user (registration)            | None           |
| `GET`    | `/users`              | Get all users                               | JWT Required   |
| `GET`    | `/user/<int:user_id>` | Get a single user by ID                     | JWT Required   |
| `PUT`    | `/user/<int:user_id>` | Update an existing user                     | JWT Required   |
| `DELETE` | `/user/<int:user_id>` | Delete a user                               | JWT Required   |
| `GET`    | `/search?name=<name>` | Search users by name (partial/case-insensitive) | JWT Required   |



# Major Issues Identified in Old Code 

- `Monolithic Structure:` All logic was in a single file (app.py), making it hard to maintain and scale.
- `Direct SQL Queries:` Used string interpolation for SQL, exposing the app to SQL injection risks.
- `No Separation of Concerns:` Business logic, database access, and routing were mixed together.
- `No Error Handling:` Errors were not handled gracefully.
- `No API Documentation:` No Swagger/OpenAPI documentation for endpoints.
- `No CORS Handling:` Cross-origin requests were not managed.
- `No Blueprint Usage:` All routes were registered directly on the app.

# Changes Made to Address Identified Issues 

- `Modularization:` Split code into folders (controllers, models, repositories, routes, usecases, middlewares, utils) for better organization and maintainability.
- `Blueprints:` Used Flask Blueprints for routing, making it easier to manage and extend endpoints.
- `Repository Pattern:` Encapsulated database logic in a repository class to avoid direct SQL in routes and improve testability.
- `Error Handling Middleware:` Added custom error handling for consistent API responses.
- `Swagger Integration:` Added Swagger UI and OpenAPI spec for API documentation and easier client integration.
- `CORS Support:` Enabled CORS to allow cross-origin requests.
- `Environment Configuration:` Centralized configuration for easier management.
- `Teardown Logic:` Ensured proper closing of database connections to avoid resource leaks. 


# Assumptions or Trade-offs

- `SQLite Used for Simplicity:` Assumed SQLite is sufficient for demo purposes; not suitable for production scale.
- `No Authentication/Authorization:` Only basic structure for - - middleware; full auth not implemented.
- `Minimal Validation:` Input validation is basic; could be improved with more time.
- `No Migrations:` Database schema changes are manual; a migration tool would be better. 

# What Would Be Done With More Time

- Implement robust authentication and authorization.
- Add automated tests for all layers.
- Use environment variables for sensitive config.
- Add database migrations and seeders.
- Improve input validation and error messages.
- Refactor for async support and scalability.
- Add logging and monitoring. 


# AI Usage

AI assistants were used as development tools during this project. The following tools were utilized:

- `ChatGPT:` Used for code generation, refactoring suggestions, and documentation drafting.
- `GitHub Copilot:` Assisted with code completion, boilerplate generation, and error handling patterns.
- `Gemini:` Provided architectural advice and code review feedback.
- `Grok:` Used for code search and understanding legacy code structure. 


# How AI Was Used

- Generated initial code for modularization, error handling, and API documentation.
- Drafted and refined documentation sections, including this CHANGES.md.
- Provided suggestions for best practices and project structure.
- Assisted in identifying and resolving major issues in the legacy code. 


# Modifications and Decisions
- All AI-generated code was reviewed and manually modified to fit project requirements and ensure correctness.
- Some AI suggestions were rejected if they did not align with project goals or best practices.
- No code was accepted without human review and testing.

# Notes on Other Tools
- Cursor was not used in this project, but is recommended for efficient and optimized code writing in future work.