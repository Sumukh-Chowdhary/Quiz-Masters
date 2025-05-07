# 🎓 Quiz Master V2

A multi-user, full-stack exam preparation platform built using Flask and Vue.js. It features role-based access (Admin & Users), real-time quiz management, scoring, scheduling, reminders, and performance reporting — all integrated with Redis, Celery, and SQLite.

---

## 📌 Features

### 👤 User Functionality
- User Registration & Login (Token-based)
- Choose subjects/chapters and attempt quizzes
- View scores and past attempts
- Export quiz results as CSV
- Receive daily quiz reminders via email/Google Chat
- Monthly performance report sent via email

### 🛠 Admin (Quiz Master)
- Predefined admin login (no registration required)
- Manage Subjects → Chapters → Quizzes → Questions (CRUD)
- Set quiz duration & date
- Monitor all user activities
- Export quiz performance for all users as CSV
- Trigger email notifications for all users
- View summary charts (e.g., quiz count, average score, top scorers)

---

## 🧱 Tech Stack

### 📦 Backend
- **Flask** with `flask-restful` for REST APIs
- **Flask-Security** for authentication & role-based access
- **SQLite** for local data storage
- **Redis** for caching and Celery queues
- **Celery** for scheduled and asynchronous jobs
- **Mailhog** for email testing
- **Google Chat Webhooks** for notifications

### 🎨 Frontend
- **Vue.js** with **Vue Router**
- **Bootstrap** for responsive UI

---

## ⚙️ Background Jobs with Celery

| Job Type         | Description |
|------------------|-------------|
| 🕰 Scheduled Job (Daily) | Sends reminder in Google Web Chat users or when new quizzes are created |
| 📅 Monthly Job  | Sends detailed performance reports to users via email |
| ⏬ Export (Async) | Admin/User can trigger CSV report export jobs (notified on completion) |

---

## 🚀 Running Locally

### Prerequisites
- Python 3.x
- Redis
- Node.js
- Mailhog (for local email testing)

### Backend Setup

```bash
# Clone repo and navigate
git clone https://github.com/yourusername/quiz-master-v2.git
cd backend/

# Create virtual environment
python -m venv venv
source venv/bin/activate  # or venv\Scripts\activate on Windows

# Install dependencies
pip install -r requirements.txt

# Start Redis
redis-server

# Start Flask server
python app.py

# Start Celery worker
celery -A app.celery worker --loglevel=info

# Start Celery beat for scheduled jobs
celery -A app.celery beat --loglevel=info
