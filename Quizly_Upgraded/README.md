# Quizly — Cloud-Based Online Quiz System

A starter full-stack college project using **Python Flask + SQLite + HTML/CSS**.

## Features
- Separate Admin and Participant login roles
- Participant registration (passwords are hashed)
- Admin dashboard with participant, quiz, and attempt counts
- Admin can create/edit/delete quizzes and add/delete MCQ questions, set a 1–180 minute timer, and add explanations
- Admin-only AI question generator (requires `OPENAI_API_KEY`)
- Participants can take quizzes and get automatic scores
- Attempt history for each participant
- Leaderboard calculated from actual attempts in the database
- Four sample quizzes are seeded automatically on first run
- Responsive layout
- Per-quiz countdown timer with automatic browser submission at zero
- Saved attempt duration and answer review with correct answers/explanations
- Participant performance analytics and quiz history
- Optional OpenAI-powered MCQ generator for admins (review before saving)
- Persistent browser dark/light theme preference
- SQLite schema migrations preserve older Quizly databases

## Run on Windows
1. Install Python 3.10 or newer.
2. Extract the ZIP.
3. Open Command Prompt/Terminal inside the extracted `quizly_full_resource` folder.
4. Create a virtual environment (recommended):
   ```bash
   python -m venv .venv
   ```
5. Activate it:
   ```bash
   .venv\Scripts\activate
   ```
6. Install requirements:
   ```bash
   pip install -r requirements.txt
   ```
7. (Optional, for the AI generator) Set an OpenAI API key in your terminal. Do not put the key in source code or commit it to GitHub.
   ```bat
   set OPENAI_API_KEY=your-api-key
   set OPENAI_MODEL=gpt-4o-mini
   ```
8. Start the app:
   ```bash
   python app.py
   ```
9. Open `http://127.0.0.1:5000` in your browser.

## Demo admin login
- Email: `admin@quizly.local`
- Password: `Admin123!`

Change these demo credentials before using the project for real users. You can set environment variables before the first launch:
- `QUIZLY_ADMIN_EMAIL`
- `QUIZLY_ADMIN_PASSWORD`
- `SECRET_KEY`

On Windows Command Prompt, for example:
```bat
set QUIZLY_ADMIN_EMAIL=your-admin-email@example.com
set QUIZLY_ADMIN_PASSWORD=choose-a-strong-password
set SECRET_KEY=replace-with-a-long-random-secret
python app.py
```
The default admin account is only seeded if that email does not already exist in the database.

## Participant login
Participants click **Create participant account**, register with name/email/password (minimum 8 characters), and then log in with the Participant role.

## Important deployment notes
- This is a functional local starter, not already hosted online.
- SQLite is suitable for local demos. For a real public cloud deployment, use a managed database such as PostgreSQL, set a strong `SECRET_KEY`, disable debug mode, configure HTTPS, add CSRF protection and rate limiting, and use a production WSGI server. Do not use the demo admin credentials on a public deployment.
- Admin-created quizzes and participant attempts are stored in `quizly.db` next to `app.py`.


## Upgrade notes
- Existing `quizly.db` is retained. On startup, `app.py` adds the new columns if missing.
- Existing quizzes default to a 10-minute timer. Edit each quiz to change its limit.
- AI question generation is optional. Without `OPENAI_API_KEY`, the rest of Quizly works normally and the generator displays setup guidance.
- AI-generated content can be wrong. Administrators should verify every question and correct answer before saving.
- The theme toggle stores the preference in the current browser.
- For Render deployment, set Build Command to `pip install -r requirements.txt` and Start Command to `gunicorn app:app`. Set `SECRET_KEY`, `QUIZLY_ADMIN_EMAIL`, `QUIZLY_ADMIN_PASSWORD`, and optionally `OPENAI_API_KEY` in Render Environment. SQLite on ephemeral hosting may not persist; use a persistent disk or managed database for important production data.
