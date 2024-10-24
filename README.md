# Go Fiber Authentication API

This project is a user authentication API built with [Go Fiber](https://gofiber.io/), PostgreSQL, and JWT (JSON Web Tokens) for secure authentication. The API allows user registration, login, and provides JWT-based session management. It uses environment variables or a configuration file for sensitive information like database credentials.

## Features

- User registration with hashed passwords.
- User login with JWT-based authentication.
- PostgreSQL for storing user data.
- CORS support for frontend API access.
- Secure configuration using environment variables.

## Prerequisites

Before you begin, ensure you have the following installed:

- [Go](https://golang.org/doc/install) (version 1.16 or later)
- [PostgreSQL](https://www.postgresql.org/download/)
- [Postman](https://www.postman.com/downloads/) (for testing the API)
- Optional: [Docker](https://www.docker.com/) (for containerized environments)

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/go-auth-fiber.git
   ```
2. Navigate to the project directory:

```bash
  cd go-auth-fiber
```
3. Install the Go dependencies:

```bash
  go mod tidy
```
4. Set up environment variables for database credentials:

  * Export them directly in your shell (for development):

```bash
export DB_USER=yourdbuser
export DB_PASSWORD=yourdbpassword
export DB_HOST=localhost
export DB_NAME=goAuthFiber
export DB_SSLMODE=disable
```
  * Alternatively, you can create a .env file in the root of your project:

```bash
DB_USER=yourdbuser
DB_PASSWORD=yourdbpassword
DB_HOST=localhost
DB_NAME=goAuthFiber
DB_SSLMODE=disable
```
5. Create the PostgreSQL database:

```bash
psql -U yourdbuser -c "CREATE DATABASE goAuthFiber;"
```
6. Run the application:

```bash
go run main.go
```
The app will start on http://localhost:3000.

## Configuration
You can configure the app using environment variables or a configuration file (config.json). The following variables can be set:

* `DB_USER`: The PostgreSQL database username.
* `DB_PASSWORD`: The PostgreSQL database password.
* `DB_HOST`: The database host (usually localhost for local development).
* `DB_NAME`: The name of the PostgreSQL database.
* `DB_SSLMODE`: The SSL mode for connecting to the database (use disable for local development).

Example config.json:
If you prefer using a config file, create a config.json file with the following structure:

```json
{
    "db_user": "yourdbuser",
    "db_password": "yourdbpassword",
    "db_host": "localhost",
    "db_name": "goAuthFiber",
    "db_sslmode": "disable"
}
```
## API Endpoints
### Register a User
POST `/register`

Request Body (JSON):

```json
{
    "username": "testuser",
    "email": "testuser@example.com",
    "password": "password123"
}
```
Response:

```json
{
    "message": "User created successfully"
}
```
### Login a User
POST `/login`

Request Body (JSON):

```json
{
    "email": "testuser@example.com",
    "password": "password123"
}
```
Response (if successful):

```json
{
    "token": "your_jwt_token_here"
}
```
### Protected Routes
You can create protected routes in Go Fiber by adding middleware for JWT verification:

```go
app.Use("/protected", middleware.JWTProtected())
```
Use the token returned from the login endpoint in the Authorization header to access protected routes.

### Example Usage with Postman
1. Register a new user by sending a POST request to `/register` with the required JSON payload.
2. Login with the same user credentials by sending a POST request to `/login`.
3. Use the returned JWT token in the Authorization header for subsequent requests to protected routes.

### Running Tests
To run tests, use the following command:

```bash
go test ./...
```
### Docker Support (Optional)
You can containerize your Go Fiber app and PostgreSQL using Docker.

1. Build and run the Docker containers:

```bash
docker-compose up --build
```
2. The app will be available at `http://localhost:3000`, and PostgreSQL will run inside a container.

### License
This project is licensed under the MIT License. See the LICENSE file for details.

### Contact
For any issues, feel free to open an issue or contact the project maintainer at amansingh.00321@gmail.com






