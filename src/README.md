# Mergington High School Activities API

A super simple FastAPI application that allows students to view and sign up for extracurricular activities.

## Features

- View all available extracurricular activities
- Teacher login to register and unregister students
- Public viewing of activity participants

## Getting Started

1. Install the dependencies:

   ```
   pip install fastapi uvicorn
   ```

2. Run the application:

   ```
   export TEACHER_CREDENTIALS='{"teacher1":"choose-a-strong-password","teacher2":"another-strong-password"}'
   python app.py
   ```

   Set this environment variable in the deployment environment as well. Add teacher accounts to the JSON object as needed; do not commit passwords to the repository. Credentials are held in the browser only until sign-out or page reload.

3. Open your browser and go to:
   - API documentation: http://localhost:8000/docs
   - Alternative documentation: http://localhost:8000/redoc

## API Endpoints

| Method | Endpoint                                                          | Description                                                         |
| ------ | ----------------------------------------------------------------- | ------------------------------------------------------------------- |
| GET    | `/activities`                                                     | Get all activities with their details and current participant count |
| POST   | `/auth/verify`                                                    | Verify teacher credentials                                          |
| POST   | `/activities/{activity_name}/signup?email=student@mergington.edu` | Teacher registers a student for an activity                         |
| DELETE | `/activities/{activity_name}/unregister?email=student@mergington.edu` | Teacher unregisters a student from an activity                    |

The verification and roster-mutation endpoints require HTTP Basic authentication using the configured teacher credentials. Activity and participant information remains publicly readable. Use HTTPS when exposing the application beyond a trusted local environment.

## Data Model

The application uses a simple data model with meaningful identifiers:

1. **Activities** - Uses activity name as identifier:

   - Description
   - Schedule
   - Maximum number of participants allowed
   - List of student emails who are signed up

2. **Students** - Uses email as identifier:
   - Name
   - Grade level

All data is stored in memory, which means data will be reset when the server restarts.
