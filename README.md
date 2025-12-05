# FastAPI Calculator with User Management & Authentication

[![CI/CD](https://github.com/Ishita-Kulkarni/assignment12/workflows/FastAPI%20User%20Management%20CI/CD/badge.svg)](https://github.com/Ishita-Kulkarni/assignment12/actions)
[![Python 3.9+](https://img.shields.io/badge/python-3.9+-blue.svg)](https://www.python.org/downloads/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.104+-green.svg)](https://fastapi.tiangolo.com/)
[![Tests](https://img.shields.io/badge/tests-59%20passing-brightgreen.svg)](https://github.com/Ishita-Kulkarni/assignment12)
[![Coverage](https://img.shields.io/badge/coverage-48%25-yellow.svg)](https://github.com/Ishita-Kulkarni/assignment12)
[![Docker](https://img.shields.io/badge/Docker-Enabled-blue.svg)](https://www.docker.com/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15-blue.svg)](https://www.postgresql.org/)
[![JWT](https://img.shields.io/badge/JWT-Authentication-orange.svg)](https://jwt.io/)

A production-ready FastAPI application featuring **JWT authentication**, **user management**, **calculator API with BREAD operations**, comprehensive integration testing (59 tests with database verification), and automated CI/CD pipeline with Docker Hub deployment.

## 🔗 Quick Links

- **GitHub Repository**: https://github.com/Ishita-Kulkarni/assignment12
- **API Documentation**: http://localhost:8000/docs (when running locally)
- **CI/CD Pipeline**: https://github.com/Ishita-Kulkarni/assignment12/actions
- **Project Structure**: [PROJECT_STRUCTURE.md](./PROJECT_STRUCTURE.md)

## What's New in Assignment 12

This project builds upon Assignment 11 with significant enhancements:

✨ **Calculator API with BREAD Operations**
- Full BREAD pattern implementation (Browse, Read, Edit, Add, Delete)
- Calculation endpoints for all basic operations (add, subtract, multiply, divide)
- User-specific calculation history
- PUT and PATCH support for updates

🔐 **JWT Token Authentication**
- Token-based authentication system using python-jose
- 30-minute token expiration
- Protected endpoints requiring valid JWT tokens
- Secure session management

🧪 **Comprehensive Integration Testing**
- **59 integration tests** (up from 18 in Assignment 11)
- **Database verification** in all integration tests
- Tests for all BREAD operations
- Invalid data and error scenario testing
- Complete test coverage for user + calculation APIs

📁 **Improved Project Organization**
- Clean folder structure with `examples/`, `data/`, `docs/`
- Demo scripts moved to `examples/` directory
- Database files properly excluded from git
- Comprehensive documentation in `PROJECT_STRUCTURE.md`

🚀 **Enhanced CI/CD**
- PostgreSQL service in GitHub Actions
- All 59 tests run on every commit
- Automatic Docker image builds on successful tests
- Multi-Python version testing (3.9-3.12)

## Features

🔐 **JWT Authentication & User Management**
- User registration with email validation
- Secure password hashing with bcrypt
- JWT token-based authentication (30-minute expiration)
- User login with token generation
- Protected endpoints requiring authentication
- Full user CRUD operations
- Unique username and email constraints

🧮 **Calculator API (BREAD Operations)**
- **Browse**: List all user's calculations with pagination
- **Read**: Get specific calculation by ID
- **Edit**: Update calculations (PUT/PATCH support)
- **Add**: Create new calculations (add, subtract, multiply, divide)
- **Delete**: Remove calculations
- User isolation (users only see their own calculations)
- Division by zero validation
- Result calculation and persistence

🔧 **API Backend**
- RESTful API with FastAPI
- SQLAlchemy ORM with PostgreSQL/SQLite
- Pydantic schemas for request/response validation
- Interactive API documentation (Swagger UI & ReDoc)
- Comprehensive logging system
- Error handling with proper HTTP status codes

🔒 **Security**
- JWT token authentication (python-jose)
- Bcrypt password hashing (bcrypt 4.0.1)
- Token-based session management
- Input validation with Pydantic
- SQL injection prevention via SQLAlchemy
- User data isolation
- Environment variable configuration

✅ **Testing & Quality**
- **59 integration tests** (all passing)
- **20 user API tests** with database verification
- **39 calculation API tests** with BREAD coverage
- Database verification in tests
- Error scenario testing
- Invalid data validation tests
- 48% code coverage from integration tests

🐳 **Docker & Database Integration**
- Docker Compose setup with FastAPI + PostgreSQL + pgAdmin
- PostgreSQL database for production
- SQLite support for development/testing
- pgAdmin for database management
- Production-ready containerization
- Multi-stage Docker builds

🚀 **CI/CD Pipeline**
- Automated testing on GitHub Actions with PostgreSQL
- Multi-version Python testing (3.9-3.12)
- All 59 integration tests run on each commit
- Docker image builds and pushes to Docker Hub on success
- Code coverage reporting
- Linting with flake8
- Automated deployment pipeline

## Quick Start with Docker

### Prerequisites
- Docker Desktop installed and running
- Git
- Docker Hub account (for pushing images)

### Setup

1. Clone the repository:
```bash
git clone https://github.com/Ishita-Kulkarni/assignment12.git
cd assignment12/assignment12
```

2. Configure environment variables:
```bash
cp .env.example .env
# Edit .env with your database credentials (or use SQLite default)
```

3. Start all services with Docker Compose:
```bash
docker compose up --build
```

4. Access the services:
   - **API Documentation (Swagger)**: http://localhost:8000/docs
   - **API Documentation (ReDoc)**: http://localhost:8000/redoc
   - **pgAdmin**: http://localhost:5050
   - **PostgreSQL**: localhost:5432

### pgAdmin Login
- Email: `admin@example.com`
- Password: `admin`

### Database Connection (in pgAdmin)
- Host: `db` (or `postgres`)
- Port: `5432`
- Database: `calculator_db`
- Username: `calculator_user`
- Password: `calculator_pass`

### Pull from Docker Hub (Optional)

Instead of building locally, you can pull the pre-built image (if available):

```bash
# Pull the latest image from Docker Hub
docker pull YOUR_DOCKERHUB_USERNAME/fastapi-calculator:latest

# Run the container with SQLite
docker run -d -p 8000:8000 \
  -e DATABASE_URL=sqlite:///./data/calculator.db \
  --name fastapi-app \
  YOUR_DOCKERHUB_USERNAME/fastapi-calculator:latest

# Or run with PostgreSQL
docker run -d -p 8000:8000 \
  -e DATABASE_URL=postgresql://calculator_user:calculator_pass@host.docker.internal:5432/calculator_db \
  --name fastapi-app \
  YOUR_DOCKERHUB_USERNAME/fastapi-calculator:latest

# Check if it's running
docker ps

# View logs
docker logs fastapi-app

# Access API docs
open http://localhost:8000/docs
```

> **Note**: Replace `YOUR_DOCKERHUB_USERNAME` with your Docker Hub username. Configure Docker Hub credentials in GitHub Secrets (`DOCKERHUB_USERNAME` and `DOCKERHUB_TOKEN`) to enable automated image pushes.

## Running Tests Locally

### Quick Start

```bash
# 1. Create and activate virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# 2. Install dependencies
pip install -r requirements.txt
pip install -r requirements-test.txt

# 3. Run all tests
pytest -v

# 4. Run with coverage report
pytest --cov=. --cov-report=html --cov-report=term-missing

# 5. View coverage report
open htmlcov/index.html  # On Linux: xdg-open htmlcov/index.html
```

### Integration Tests (59 Tests)

The project includes comprehensive integration tests that verify the API against a real database.

#### Run All Integration Tests

```bash
# Run all user and calculation integration tests
pytest tests/test_users.py tests/test_calculations_api.py -v

# Expected output: 59 passed (20 user tests + 39 calculation tests)
```

#### User Integration Tests (20 tests)

```bash
# Run user integration tests
pytest tests/test_users.py -v

# What's tested:
# ✓ User registration with DB verification
# ✓ User login with JWT tokens and DB validation
# ✓ Password hashing (bcrypt)
# ✓ Duplicate username/email prevention
# ✓ Email/password validation
# ✓ User CRUD operations
```

#### Calculation Integration Tests (39 tests)

```bash
# Run calculation integration tests
pytest tests/test_calculations_api.py -v

# What's tested:
# ✓ Create calculations with DB verification
# ✓ Browse calculations (pagination, user isolation)
# ✓ Read specific calculations
# ✓ Update calculations (PUT/PATCH) with DB verification
# ✓ Delete calculations with DB verification
# ✓ Division by zero validation
# ✓ Invalid data handling
# ✓ Authentication requirements
# ✓ Error responses (400, 401, 403, 404, 422)
```

#### Run Specific Test Categories

```bash
# Authentication tests (12 tests)
pytest tests/test_auth.py -v

# Schema validation tests (20 tests)
pytest tests/test_schemas.py -v

# Model tests (10 tests)
pytest tests/test_models.py -v

# Calculator operations tests (37 tests)
pytest tests/test_operations.py -v

# Run specific test function
pytest tests/test_users.py::TestUserRegistration::test_register_user_db_verification -v
```

### Expected Test Results

✅ **59 integration tests** should pass (20 user + 39 calculation)  
✅ **48% coverage** from integration tests alone  
✅ **100% coverage** on `schemas.py`  
✅ **90% coverage** on `users.py`  
✅ **80% coverage** on `calculations.py`  

### Test Output Example

```
tests/test_users.py::TestUserRegistration::test_register_user_success PASSED        [  1%]
tests/test_users.py::TestUserRegistration::test_register_user_db_verification PASSED [  3%]
tests/test_users.py::TestUserLogin::test_login_db_verification PASSED               [  5%]
...
tests/test_calculations_api.py::TestCalculationAdd::test_add_calculation_success PASSED
tests/test_calculations_api.py::TestCalculationBrowse::test_browse_calculations_db_verification PASSED
tests/test_calculations_api.py::TestInvalidDataAndErrors::test_division_by_zero_error_response PASSED

==================== 59 passed in 41.00s ====================
```

## Manual Testing via OpenAPI (Swagger UI)

The application provides interactive API documentation where you can test all endpoints manually.

### Access OpenAPI Documentation

1. **Start the application**:
   ```bash
   # Using Docker Compose (recommended)
   docker compose up
   
   # OR using uvicorn directly
   uvicorn app.main:app --reload
   ```

2. **Open Swagger UI** in your browser:
   - **Swagger UI**: http://localhost:8000/docs
   - **ReDoc** (alternative): http://localhost:8000/redoc

### Step-by-Step Manual Testing

#### 1. Register a New User

1. Open http://localhost:8000/docs
2. Expand **POST /users/register**
3. Click **"Try it out"**
4. Enter request body:
   ```json
   {
     "username": "testuser",
     "email": "test@example.com",
     "password": "password123"
   }
   ```
5. Click **"Execute"**
6. Verify response:
   - Status Code: **201 Created**
   - Response includes: `id`, `username`, `email`, `created_at`
   - Password is NOT returned (security check ✓)

#### 2. Login to Get JWT Token

1. Expand **POST /users/login**
2. Click **"Try it out"**
3. Enter credentials:
   ```json
   {
     "username": "testuser",
     "password": "password123"
   }
   ```
4. Click **"Execute"**
5. Verify response:
   - Status Code: **200 OK**
   - Response includes: `access_token`, `token_type: "bearer"`
6. **Copy the access_token** (you'll need it for protected endpoints)

#### 3. Authorize Your Session

1. Click the **"Authorize"** button (🔓 icon) at the top right
2. Paste your token in the format: `Bearer YOUR_TOKEN_HERE`
3. Click **"Authorize"**
4. Click **"Close"**
5. Now all requests will include authentication!

#### 4. Test Protected Endpoint - Get Current User

1. Expand **GET /users/me**
2. Click **"Try it out"** → **"Execute"**
3. Verify response:
   - Status Code: **200 OK**
   - Returns your user information

#### 5. Create a Calculation

1. Expand **POST /calculations**
2. Click **"Try it out"**
3. Enter calculation:
   ```json
   {
     "a": 10.5,
     "b": 5.2,
     "type": "add"
   }
   ```
4. Click **"Execute"**
5. Verify response:
   - Status Code: **201 Created**
   - Response includes: `id`, `result: 15.7`, `user_id`
6. **Copy the calculation ID** for next steps

#### 6. Browse All Your Calculations

1. Expand **GET /calculations**
2. Click **"Try it out"** → **"Execute"**
3. Verify response:
   - Status Code: **200 OK**
   - Returns array of your calculations
   - Ordered by creation date (newest first)

#### 7. Read a Specific Calculation

1. Expand **GET /calculations/{id}**
2. Enter the calculation ID from step 5
3. Click **"Execute"**
4. Verify response:
   - Status Code: **200 OK**
   - Returns the specific calculation

#### 8. Update a Calculation (PUT)

1. Expand **PUT /calculations/{id}**
2. Enter the calculation ID
3. Enter new values:
   ```json
   {
     "a": 20,
     "b": 4,
     "type": "multiply"
   }
   ```
4. Click **"Execute"**
5. Verify response:
   - Status Code: **200 OK**
   - Result updated to: **80** (20 × 4)

#### 9. Partial Update (PATCH)

1. Expand **PATCH /calculations/{id}**
2. Enter the calculation ID
3. Update only one field:
   ```json
   {
     "b": 5
   }
   ```
4. Click **"Execute"**
5. Verify response:
   - Previous values preserved (`a: 20`, `type: multiply`)
   - Only `b` changed to 5
   - Result recalculated to: **100** (20 × 5)

#### 10. Delete a Calculation

1. Expand **DELETE /calculations/{id}**
2. Enter the calculation ID
3. Click **"Execute"**
4. Verify response:
   - Status Code: **200 OK**
   - Message: "Calculation X deleted successfully"
5. Try to GET the same calculation:
   - Status Code: **404 Not Found**

### Test Error Scenarios

#### Division by Zero

1. Expand **POST /calculations**
2. Try creating:
   ```json
   {
     "a": 10,
     "b": 0,
     "type": "divide"
   }
   ```
3. Verify response:
   - Status Code: **422 Unprocessable Entity**
   - Error message about division by zero

#### Invalid Operation Type

1. Try creating with invalid type:
   ```json
   {
     "a": 10,
     "b": 5,
     "type": "power"
   }
   ```
2. Verify response:
   - Status Code: **422 Unprocessable Entity**
   - Validation error

#### Authentication Required

1. Click **"Authorize"** → **"Logout"**
2. Try **POST /calculations** without authentication
3. Verify response:
   - Status Code: **403 Forbidden**

### Automated Manual Testing Script

For quick verification, run the automated manual test script:

```bash
# Ensure server is running first
uvicorn app.main:app --reload

# In another terminal, run the test script
python examples/test_api_manual.py
```

**Expected output**:
```
🧪 TEST 1: Register User (POST /users/register)
✅ PASS: User registered successfully

🧪 TEST 2: Login User (POST /users/login)
✅ PASS: User logged in, token received

🧪 TEST 3: Get Current User (GET /users/me)
✅ PASS: Current user retrieved

... (13 tests total)

🎉 ALL TESTS PASSED!
```

### Troubleshooting Tests

If tests fail:

```bash
# Ensure correct bcrypt version (CRITICAL)
pip install bcrypt==4.0.1

# Clear pytest cache
rm -rf .pytest_cache __pycache__

# Reinstall dependencies
pip install -r requirements.txt -r requirements-test.txt

# Run tests with verbose output
pytest -vv --tb=short
```

## SQL Database Setup

All SQL scripts are in the `sql/` directory:
- `01_create_tables.sql` - Create users and calculations tables
- `02_insert_records.sql` - Insert sample data
- `03_query_data.sql` - Query and join operations
- `04_update_record.sql` - Update records
- `05_delete_record.sql` - Delete records
- `complete_setup.sql` - Run all steps at once

See [sql/README.md](sql/README.md) for detailed SQL documentation.

## Requirements

- Python 3.7+
- FastAPI
- Uvicorn
- Pydantic
- Docker & Docker Compose (for containerized setup)
- PostgreSQL 15 (via Docker)

## Installation (Local Development)

1. Create a virtual environment (recommended):
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

## Running the Application

Start the server:
```bash
python main.py
```

Or use uvicorn directly:
```bash
uvicorn main:app --reload
```

The application will be available at: `http://localhost:8000`

## Using the Calculator

Once the server is running, visit:
- **Web Calculator**: `http://localhost:8000` - Interactive calculator interface
- **API Docs**: `http://localhost:8000/docs` - Swagger UI for API testing
- **Alternative Docs**: `http://localhost:8000/redoc` - ReDoc documentation
- **API Info**: `http://localhost:8000/api` - API information endpoint

### Web Interface
Simply open your browser and navigate to `http://localhost:8000`. You'll see a beautiful calculator interface where you can:
1. Enter two numbers
2. Select an operation (Add, Subtract, Multiply, Divide)
3. Click "Calculate" or press Enter
4. See the result displayed instantly

## API Endpoints

### User Management

#### POST /users/register
Register a new user with username, email, and password.

**Request Body:**
```json
{
  "username": "johndoe",
  "email": "john@example.com",
  "password": "securePassword123"
}
```

**Response:**
```json
{
  "id": 1,
  "username": "johndoe",
  "email": "john@example.com",
  "created_at": "2024-01-15T10:30:00",
  "is_active": true
}
```

#### POST /users/login
Authenticate user with username and password.

**Request Body:**
```json
{
  "username": "johndoe",
  "password": "securePassword123"
}
```

**Response:**
```json
{
  "message": "Login successful",
  "user": {
    "id": 1,
    "username": "johndoe",
    "email": "john@example.com"
  }
}
```

#### GET /users
Get all users (paginated).

**Query Parameters:**
- `skip`: Number of records to skip (default: 0)
- `limit`: Maximum number of records (default: 100)

#### GET /users/{user_id}
Get a specific user by ID.

#### PUT /users/{user_id}
Update user information.

**Request Body:**
```json
{
  "email": "newemail@example.com"
}
```

#### DELETE /users/{user_id}
Delete a user.

### Calculator Endpoints

#### POST /calculate
Performs arithmetic calculations.

**Request Body:**
```json
{
  "num1": 10,
  "num2": 5,
  "operation": "add"
}
```

**Supported Operations:**
- `add` - Addition
- `subtract` - Subtraction
- `multiply` - Multiplication
- `divide` - Division

**Response:**
```json
{
  "result": 15.0,
  "operation": "add",
  "num1": 10.0,
  "num2": 5.0
}
```

### Health Check

#### GET /health
Returns application health status.

## Example Usage

Using curl:

### User Registration
```bash
curl -X POST "http://localhost:8000/users/register" \
  -H "Content-Type: application/json" \
  -d '{
    "username": "johndoe",
    "email": "john@example.com",
    "password": "securePassword123"
  }'
```

### User Login
```bash
curl -X POST "http://localhost:8000/users/login" \
  -H "Content-Type: application/json" \
  -d '{
    "username": "johndoe",
    "password": "securePassword123"
  }'
```

### Get All Users
```bash
curl -X GET "http://localhost:8000/users?skip=0&limit=10"
```

### Calculator Operations
```bash
# Addition
curl -X POST "http://localhost:8000/calculate" \
  -H "Content-Type: application/json" \
  -d '{"num1": 10, "num2": 5, "operation": "add"}'

# Division
curl -X POST "http://localhost:8000/calculate" \
  -H "Content-Type: application/json" \
  -d '{"num1": 20, "num2": 4, "operation": "divide"}'
```

## Error Handling

The API handles common errors:
- Division by zero returns a 400 error
- Invalid operations return a 400 error with supported operations list
- Invalid input types are caught by Pydantic validation

## Testing

The project includes comprehensive tests covering 60 test cases:

### Test Categories
- **Authentication Tests** (`tests/test_auth.py`): 12 tests for password hashing
- **Schema Tests** (`tests/test_schemas.py`): 20 tests for Pydantic validation
- **Model Tests** (`tests/test_models.py`): 10 tests for SQLAlchemy User model
- **Integration Tests** (`tests/test_users.py`): 18 tests for API endpoints
- **Calculator Tests** (`tests/test_operations.py`): 37 tests for calculator functions
- **API Tests** (`tests/test_main.py`): 37 tests for calculator API endpoints
- **Logging Tests** (`tests/test_logging.py`): 26 tests for logging system

### Running Tests

Install test dependencies:
```bash
pip install -r requirements-test.txt
```

Run all tests:
```bash
pytest -v
```

Run with coverage:
```bash
pytest --cov=. --cov-report=html --cov-report=term-missing
```

Run specific test categories:
```bash
# User management tests
pytest tests/test_auth.py tests/test_schemas.py tests/test_models.py tests/test_users.py -v

# Calculator tests
pytest tests/test_operations.py tests/test_main.py -v

# All tests with coverage
pytest -v --cov=. --cov-report=xml --cov-report=term-missing
```

### Test Coverage
Current test coverage: **75%**
- `auth.py`: 100%
- `schemas.py`: 100%
- `models.py`: 100%
- `users.py`: 93%
- `operations.py`: 100%
- `main.py`: 100%

## Logging

The application includes comprehensive logging to track operations and errors.

### Log Files
- `logs/app.log` - All application logs (DEBUG, INFO, WARNING, ERROR)
- `logs/error.log` - Error logs only (ERROR, CRITICAL)

### What Gets Logged
- ✓ All HTTP requests and responses with duration
- ✓ Calculator operations (inputs and results)
- ✓ Errors and exceptions with full stack traces
- ✓ Application startup and shutdown events

### Log Rotation
- Max file size: 10 MB
- Backup count: 5 files
- Automatic rotation when size limit is reached

### Viewing Logs
```bash
# View all logs
cat logs/app.log

# View errors only
cat logs/error.log

# Follow logs in real-time
tail -f logs/app.log
```

For detailed logging documentation, see [LOGGING.md](LOGGING.md)

## CI/CD Pipeline

The project features a comprehensive CI/CD pipeline with GitHub Actions that automatically tests and deploys your application.

### Pipeline Overview

```mermaid
graph LR
    A[Push to Main] --> B[Run Tests]
    B --> C{Tests Pass?}
    C -->|Yes| D[Build Docker Image]
    C -->|No| E[Pipeline Fails]
    D --> F[Push to Docker Hub]
    F --> G[Deployment Ready]
```

### What Happens on Push

1. **Testing Phase** (runs on every push/PR)
   - Tests run on Python 3.9, 3.10, 3.11, and 3.12
   - PostgreSQL service spins up for integration tests
   - All 60+ tests execute with coverage reporting
   - Code linting with flake8
   - Coverage report uploaded to Codecov
   - Test results archived as artifacts

2. **Build & Push Phase** (only on main branch)
   - Docker image built with multi-stage build
   - Image tagged with branch name, commit SHA, and `latest`
   - Image pushed to Docker Hub
   - Build cache optimized for faster builds

3. **Verification Phase**
   - Confirms successful deployment
   - Logs image digest for tracking

### Setting Up CI/CD

#### 1. GitHub Secrets Configuration

Add these secrets to your GitHub repository (`Settings > Secrets and variables > Actions`):

- `DOCKERHUB_USERNAME`: Your Docker Hub username
- `DOCKERHUB_TOKEN`: Docker Hub access token (not password!)

**Creating a Docker Hub Access Token:**
1. Log in to [Docker Hub](https://hub.docker.com/)
2. Go to Account Settings > Security
3. Click "New Access Token"
4. Name it (e.g., "GitHub Actions")
5. Copy the token immediately (you won't see it again!)
6. Add it as `DOCKERHUB_TOKEN` secret in GitHub

#### 2. Update Workflow File

Edit `.github/workflows/ci.yml` and replace image references:
```yaml
images: YOUR_DOCKERHUB_USERNAME/fastapi-user-management
```

#### 3. Enable GitHub Actions

Ensure GitHub Actions are enabled for your repository:
- Go to repository Settings > Actions > General
- Select "Allow all actions and reusable workflows"

### CI/CD Features

✅ **Multi-Python Version Testing**
- Tests run on Python 3.9, 3.10, 3.11, and 3.12
- Ensures compatibility across versions

✅ **Database Integration**
- PostgreSQL service container for realistic testing
- Separate test database for isolation

✅ **Code Quality**
- Flake8 linting for syntax and style
- Coverage reporting with Codecov integration

✅ **Automated Docker Deployment**
- Only deploys on successful tests
- Only runs on main branch pushes
- Supports multiple tags (latest, SHA, branch)

✅ **Build Optimization**
- Docker layer caching for faster builds
- Multi-stage builds for smaller images

### Workflow Jobs

#### `test` Job
Runs comprehensive test suite across multiple Python versions:
```yaml
- Lint with flake8
- Run unit tests (auth, schemas, models, operations)
- Run integration tests (users, calculator API)
- Run logging tests
- Generate coverage reports
- Upload to Codecov
- Archive test results and logs
```

#### `build-and-push` Job
Builds and publishes Docker image:
```yaml
- Checkout code
- Set up Docker Buildx
- Log in to Docker Hub
- Extract metadata (tags, labels)
- Build and push image
- Cache layers for optimization
```

#### `verify-deployment` Job
Confirms successful deployment:
```yaml
- Verify image pushed
- Display image digest
- Confirm pipeline completion
```

### Viewing CI/CD Results

1. **GitHub Actions Tab**: See workflow runs, logs, and status
2. **Commit Status**: Green checkmark or red X on commits
3. **Pull Requests**: Automatic status checks before merge
4. **Docker Hub**: View published images with tags

### Triggering Workflows

Workflows trigger automatically on:
- Push to `main` branch (full pipeline with Docker push)
- Push to `develop` branch (tests only)
- Pull requests to `main` or `develop` (tests only)

Manual trigger:
```bash
# Go to Actions tab > Select workflow > Run workflow
```

### Docker Image Tags

Images are tagged with:
- `latest`: Most recent build from main branch
- `main-<sha>`: Specific commit on main branch
- `main`: Latest main branch build

Example:
```bash
docker pull YOUR_USERNAME/fastapi-user-management:latest
docker pull YOUR_USERNAME/fastapi-user-management:main-a1b2c3d
```

### Troubleshooting CI/CD

**Tests failing in CI but passing locally?**
- Check Python version compatibility
- Verify environment variables are set
- Review PostgreSQL connection settings

**Docker push failing?**
- Verify `DOCKERHUB_USERNAME` and `DOCKERHUB_TOKEN` secrets
- Check Docker Hub token hasn't expired
- Ensure repository name matches Docker Hub repository

**Build taking too long?**
- Build cache should speed up subsequent builds
- First build may take 5-10 minutes
- Later builds typically 2-3 minutes

### Local Testing Before Push

Test locally before pushing:
```bash
# Run tests
pytest -v --cov=.

# Build Docker image
docker build -t fastapi-user-management:test .

# Test Docker image
docker run -p 8000:8000 fastapi-user-management:test
```

### Continuous Deployment

To add automatic deployment to a hosting platform:
1. Add deployment job to workflow
2. Configure platform credentials as secrets
3. Add deployment step after successful Docker push

Example platforms:
- AWS ECS/Fargate
- Google Cloud Run
- Azure Container Instances
- DigitalOcean App Platform
- Heroku Container Registry

## Project Structure

> **📁 Detailed structure documentation**: See [PROJECT_STRUCTURE.md](./PROJECT_STRUCTURE.md)

```
assignment12/
├── app/                        # Application code
│   ├── auth.py                 # JWT authentication & password hashing
│   ├── calculations.py         # Calculation BREAD endpoints
│   ├── database.py             # Database configuration
│   ├── main.py                 # FastAPI application entry point
│   ├── models.py               # User & Calculation models
│   ├── operations.py           # Calculator operations
│   ├── schemas.py              # Pydantic validation schemas
│   └── users.py                # User management endpoints
├── tests/                      # Test suite (59 integration tests)
│   ├── test_auth.py            # Authentication tests
│   ├── test_calculations.py    # Calculation logic tests
│   ├── test_calculations_api.py # Calculation API tests (39 tests)
│   ├── test_models.py          # Database model tests
│   ├── test_operations.py      # Calculator operation tests
│   ├── test_schemas.py         # Schema validation tests
│   ├── test_users.py           # User API tests (20 tests)
│   └── ...                     # Additional test files
├── examples/                   # Demo scripts & examples
│   ├── demo_user_endpoints.py  # User API demo
│   ├── test_api_manual.py      # Manual API testing
│   └── test_jwt_token.py       # JWT testing utility
├── docs/                       # Documentation
│   ├── CI_CD_SETUP.md          # CI/CD setup guide
│   ├── LOGGING.md              # Logging documentation
│   └── ...                     # Additional documentation
├── data/                       # Local database files (gitignored)
├── scripts/                    # Utility scripts
├── .github/workflows/          # CI/CD pipelines
│   └── ci.yml                  # Main CI/CD with PostgreSQL
├── Dockerfile                  # Docker image definition
├── docker-compose.yml          # Multi-container setup
├── requirements.txt            # Production dependencies
├── requirements-test.txt       # Testing dependencies
└── PROJECT_STRUCTURE.md        # Detailed structure documentation
```

**Key Changes from Assignment 11**:
- ✨ Added `calculations.py` with full BREAD operations
- ✨ Added JWT authentication in `auth.py`
- ✨ Enhanced test suite (59 tests with DB verification)
- ✨ Organized demo scripts in `examples/`
- ✨ Added `data/` directory for local databases
- ✨ Improved CI/CD with Docker Hub integration

## Environment Variables

The application uses environment variables for configuration. Copy `.env.example` to `.env` and configure:

### Required Variables

```bash
# Database Configuration (choose one)
# For SQLite (development/testing)
DATABASE_URL=sqlite:///./data/calculator.db

# For PostgreSQL (production)
DATABASE_URL=postgresql://calculator_user:calculator_pass@db:5432/calculator_db

# PostgreSQL Configuration (if using PostgreSQL)
POSTGRES_USER=calculator_user
POSTGRES_PASSWORD=calculator_pass
POSTGRES_DB=calculator_db
```

### Security Variables

```bash
# JWT Secret Key (REQUIRED - generate a secure random string)
SECRET_KEY=your-secret-key-here-replace-in-production

# JWT Algorithm
ALGORITHM=HS256

# JWT Token Expiration (in minutes)
ACCESS_TOKEN_EXPIRE_MINUTES=30
```

### Optional Variables

```bash
# Application Configuration
APP_NAME=FastAPI Calculator
APP_VERSION=1.0.0
DEBUG=False

# CORS Configuration
ALLOWED_ORIGINS=http://localhost:3000,http://localhost:8000
```

### Docker Hub Variables (CI/CD only)

Set these as **GitHub Secrets** (not in `.env`):
```bash
DOCKERHUB_USERNAME=your-dockerhub-username
DOCKERHUB_TOKEN=your-dockerhub-access-token
```

### Generating a Secure Secret Key

```bash
# Python method
python -c "import secrets; print(secrets.token_urlsafe(32))"

# OpenSSL method
openssl rand -hex 32
```

## Security Best Practices

### Password Security
✅ **Bcrypt Hashing**
- All passwords hashed with bcrypt (cost factor 12)
- Never store plain text passwords
- Password verification uses constant-time comparison

✅ **Version Compatibility**
- Use bcrypt 4.0.1 (not 5.0.0) for passlib compatibility
- Tested across Python 3.9-3.12

### Database Security
✅ **SQLAlchemy ORM**
- Prevents SQL injection via parameterized queries
- Input validation through Pydantic schemas

✅ **Unique Constraints**
- Usernames and emails must be unique
- Database-level constraint enforcement

### API Security
✅ **Input Validation**
- Email format validation
- Username/password requirements
- Type checking with Pydantic

✅ **Error Handling**
- No sensitive information in error messages
- Proper HTTP status codes

### Docker Security
✅ **Non-root User**
- Container runs as non-root user
- Minimal attack surface

✅ **Environment Variables**
- Sensitive data via environment variables
- `.env` file gitignored

### CI/CD Security
✅ **Secrets Management**
- Docker Hub credentials in GitHub Secrets
- Never commit secrets to repository

✅ **Dependency Scanning**
- Automated dependency updates
- Regular security audits

## Deployment

### Using Docker Hub Image

Pull and run the pre-built image:
```bash
# Pull latest image
docker pull YOUR_USERNAME/fastapi-user-management:latest

# Run with environment variables
docker run -p 8000:8000 \
  -e DATABASE_URL=postgresql://user:pass@host:5432/db \
  YOUR_USERNAME/fastapi-user-management:latest
```

### Production Deployment Checklist

- [ ] Set strong `POSTGRES_PASSWORD`
- [ ] Configure `SECRET_KEY` for JWT (future feature)
- [ ] Set `DEBUG=False`
- [ ] Configure CORS for your domain
- [ ] Set up SSL/TLS certificates
- [ ] Configure database backups
- [ ] Set up monitoring and logging
- [ ] Configure rate limiting
- [ ] Set up health checks

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Make your changes
4. Run tests (`pytest -v`)
5. Commit your changes (`git commit -m 'Add amazing feature'`)
6. Push to the branch (`git push origin feature/amazing-feature`)
7. Open a Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

- FastAPI framework by Sebastián Ramírez
- SQLAlchemy ORM
- Pydantic validation library
- bcrypt password hashing
- PostgreSQL database
- Docker containerization
- GitHub Actions CI/CD

## Support

For issues, questions, or contributions:
- Open an issue on GitHub
- Check existing documentation
- Review test examples

## Changelog

### Version 1.0.0 (Current)
- ✅ User management system with SQLAlchemy
- ✅ Secure password hashing with bcrypt
- ✅ Comprehensive test suite (60+ tests)
- ✅ CI/CD pipeline with GitHub Actions
- ✅ Docker Hub automated deployment
- ✅ PostgreSQL database integration
- ✅ Calculator API (legacy feature)
- ✅ 75% test coverage

### Future Enhancements
- [ ] JWT authentication
- [ ] User roles and permissions
- [ ] Password reset functionality
- [ ] Email verification
- [ ] Rate limiting
- [ ] API versioning
- [ ] Swagger UI customization
- [ ] Monitoring and metrics
