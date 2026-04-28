# Final Project IS 601 - Advanced Feature & Finalized Application

## Project Overview

## Final Project Enhancement

For the final project, I extended the application by adding an exponentiation calculation type. This feature was integrated across the full stack, including the backend calculation logic, schema validation, front end selection options, edit page preview behavior, and automated testing.

To support this enhancement, I added:
- calculation model logic for exponentiation
- schema support and validation for the new calculation type
- front-end integration on the dashboard and edit workflow
- unit, integration, and E2E test coverage for exponentiation

This allowed me to build on the existing calculator application without changing the overall architecture, while still adding a meaningful new feature.

## How to Use the Exponentiation Feature
The exponentiation feature can be used from the main dashboard just like the other calculation types.

### Steps
1. Log in to the application.
2. Go to the **Dashboard**.
3. In the **Operation Type** dropdown, select **Exponentiation**.
4. In the **Numbers** field, enter two or more numbers separated by commas.
5. Click **Calculate**.

### Example
- Input: `2, 4`
- Result: `16`

### Multiple Inputs
If multiple values are entered, the application evaluates exponentiation from left to right.

### Notes
- At least two numeric inputs are required.
- Inputs must be comma-separated.
- The exponentiation operation is available in the dashboard creation form and is also supported in the edit calculation preview.

### Authentication
- User registration
- User login with JWT-based authentication
- Protected routes for authenticated users
- Password hashing using bcrypt

### Calculation Management (BREAD)
- **Browse** all saved calculations for the logged-in user
- **Read** individual calculation details
- **Edit** existing calculations
- **Add** new calculations
- **Delete** calculations

### Additional Feature
- **Profile Management**
  - View current user profile with `GET /users/me`
  - Update first name, last name, and email with `PUT /users/me`

## Tech Stack

- **Backend:** FastAPI
- **Database:** PostgreSQL
- **ORM:** SQLAlchemy
- **Authentication:** JWT
- **Testing:** Pytest
- **E2E Testing:** Playwright / Requests-based E2E tests
- **Containerization:** Docker / Docker Compose
- **CI/CD:** GitHub Actions
- **Security Scanning:** Trivy
- **Admin Tool:** pgAdmin

## Project Structure

```text
app/
  auth/
  core/
  models/
  schemas/
  main.py
templates/
tests/
  unit/
  integration/
  e2e/
docker-compose.yml
Dockerfile
requirements.txt
README.md

To run prject locally:
1. Clone the repository:
git clone git@github.com:danielleev33/is601_final_project.git
cd module14_is601

2. Start the application:
docker compose up --build -d

3. Open the app:
App: http://127.0.0.1:8000
Swagger Docs: http://127.0.0.1:8000/docs
pgAdmin: http://127.0.0.1:5050

Web Routes
/ - landing page
/register - user registration page
/login - login page
/dashboard - main calculations dashboard
/dashboard/view/{calc_id} - view a specific calculation
/dashboard/edit/{calc_id} - edit a specific calculation

API Routes
Auth
POST /auth/register
POST /auth/login
POST /auth/token

Calculations
GET /calculations
POST /calculations
GET /calculations/{calc_id}
PUT /calculations/{calc_id}
DELETE /calculations/{calc_id}

User Profile
GET /users/me
PUT /users/me

Running Tests
Run the full test suite:
docker compose exec web pytest -v

Run tests without coverage plugin issues:
docker compose exec web pytest -p no:cov -o addopts='' -v

Run unit tests only:
docker compose exec web pytest -p no:cov -o addopts='' tests/unit -v

Run integration tests only:
docker compose exec web pytest -p no:cov -o addopts='' tests/integration -v

Run E2E tests only:
docker compose exec web pytest -p no:cov -o addopts='' tests/e2e/test_fastapi_calculator.py -v

Docker Hub Image:
danielleev33/is601_final_project

DockerHub Repository:
https://hub.docker.com/repository/docker/danielleev33/is601_final_project/general

During development I made some updates to get everything fully working:
- updated dependencies flagged by Trivy
- replaced python-jose w/ PyJWT for cleaner JWT handling
- fixed Swagger auth to use correct token endpoint
- made Redis blacklist checks fail safely when Redis is unavailable for testing
- added the profile management feature as required feature
- verified calculation BREAD functionality through testing

Screenshots Included:
calculation dashboard w/ BREAD functionality
calculation details/ read page
profile feature working through successful PUT /users/me update
successful GitHub Actions pipeline
Docker Hub image deployment