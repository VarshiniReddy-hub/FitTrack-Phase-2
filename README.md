# FitTrack – Phase 2: Advanced Tracking & User Engagement

A full-stack fitness platform built with FastAPI, SQLite, SQLAlchemy, JWT, React, Vite, and Recharts.

## Phase 1 features retained
- JWT registration/login and protected API requests
- Workout journal (create, view, edit, delete)
- Fitness goals and progress updates
- Daily summaries, weekly/monthly analytics, notifications

## Phase 2 features
- **Workout plans:** schedule, list, and delete upcoming sessions
- **Exercise library:** seeded Cardio, Strength, and Yoga catalogue; search/filter; add an exercise to today's workout journal
- **Progress comparison:** weekly and monthly comparison of workouts, calories, and active minutes
- **Streak tracking:** current and longest consecutive-day workout streak
- **Achievement badges:** automatic milestone awards for workouts, streaks, and completed goals
- **Personalized dashboard:** daily activity, upcoming plans, and streak summary

## Requirements
- Python 3.10+
- Node.js 18+ and npm

## Run backend (Windows PowerShell)
```powershell
cd FitTrack\backend
py -3 -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install -r requirements.txt
Copy-Item .env.example .env
uvicorn app.main:app --reload --port 8000
```
Open Swagger: http://127.0.0.1:8000/docs

If PowerShell blocks activation:
```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
.\.venv\Scripts\Activate.ps1
```

## Run frontend (second PowerShell terminal)
```powershell
cd FitTrack\frontend
npm install
npm run dev
```
Open http://localhost:5173

## Phase 2 API endpoints
- `GET|POST /api/workout-plans`
- `DELETE /api/workout-plans/{plan_id}`
- `GET /api/exercises?search=&category=`
- `POST /api/exercises/{exercise_id}/add-to-workouts`
- `GET /api/analytics/comparison?period=weekly|monthly`
- `GET /api/streak`
- `GET /api/badges`
- `GET /api/dashboard/summary`

All Phase 2 user-specific endpoints require a valid JWT. Workout plans, streaks, and earned badges are scoped to the authenticated user. The exercise catalogue is shared and read-only.

## Suggested Swagger test sequence
1. Register and log in using `/api/auth/register` and `/api/auth/login`.
2. Click **Authorize** in Swagger and enter the access token as `Bearer <token>` if prompted.
3. Create a workout plan with a future `scheduled_date`.
4. Search exercises using `/api/exercises?search=walk` and add one to today's workouts.
5. Add workouts on consecutive dates to test streak calculation.
6. Complete a goal and check `/api/badges`.
7. Check weekly/monthly comparisons and `/api/dashboard/summary`.

## Database and configuration
- `fittrack.db` is created automatically when the backend starts. New Phase 2 tables are created without deleting existing Phase 1 tables/data.
- `.env` is local configuration and must not be committed. Replace `SECRET_KEY` with a long random value before deployment.
- The ZIP intentionally excludes the local `.env`, SQLite database, virtual environment, and `node_modules`. Back up your Phase 1 database before upgrading an existing local installation.
- This is a learning/demo project, not a medical device. Calorie values are user-entered estimates.
