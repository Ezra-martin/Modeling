# AI-Powered Mental Health Chat Assistant

A full-stack web application providing AI-powered mental health support with crisis detection, resource library, and progress tracking.

## Tech Stack

- **Backend**: FastAPI (Python)
- **Frontend**: HTML, CSS, JavaScript
- **Database**: PostgreSQL
- **ORM**: SQLAlchemy
- **Authentication**: JWT

## Features

### User Features
- User registration and login with JWT authentication
- AI chat interaction with quick-reply buttons
- Mental health resource library (categories: Anxiety, Stress, Depression, etc.)
- Crisis detection with automatic emergency hotline messages
- Progress tracking (chat history, mood patterns)
- Feedback system (rating and suggestions)

### Admin Features
- Admin dashboard
- Manage mental health resources (add/edit/delete)
- View system logs (chat summaries, crisis triggers, feedback)

## Project Structure

```
/backend
    /api
    /models
    /services
    /routes
    /auth
    /database
/frontend
    /pages
    /components
    /styles
```

## Setup Instructions

### Prerequisites
- Python 3.9+
- PostgreSQL 12+
- pip

### Backend Setup

1. Navigate to backend directory:
```bash
cd backend
```

2. Create virtual environment:
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

4. Create `.env` file in `backend` directory (see `.env.example`):
```env
DATABASE_URL=postgresql://username:password@localhost:5432/mentalhealth_db
SECRET_KEY=your-secret-key-here-change-in-production
ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=30
```

5. Create PostgreSQL database:
```sql
CREATE DATABASE mentalhealth_db;
```

6. Run database migrations:
```bash
python -m alembic upgrade head
```

7. Seed initial data:
```bash
python seed_data.py
```

8. Start the backend server:
```bash
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

The API will be available at `http://localhost:8000`
API documentation: `http://localhost:8000/docs`

### Frontend Setup

1. Navigate to frontend directory:
```bash
cd frontend
```

2. Open `index.html` in a web browser, or use a local server:
```bash
# Using Python
python -m http.server 8080

# Using Node.js (if http-server is installed)
npx http-server -p 8080
```

3. Open `http://localhost:8080` in your browser

## Test Accounts

- **User**: 
  - Email: `user@test.com`
  - Password: `123456`

- **Admin**: 
  - Email: `admin@test.com`
  - Password: `admin123`

## API Endpoints

### Authentication
- `POST /api/auth/register` - User registration
- `POST /api/auth/login` - User login
- `GET /api/auth/me` - Get current user info

### Chat
- `POST /api/chat/message` - Send message to AI
- `GET /api/chat/history` - Get chat history
- `DELETE /api/chat/history/{chat_id}` - Delete chat entry

### Resources
- `GET /api/resources` - Get all resources
- `GET /api/resources/{resource_id}` - Get specific resource
- `GET /api/resources/category/{category}` - Get resources by category

### Feedback
- `POST /api/feedback` - Submit feedback
- `GET /api/feedback` - Get user's feedback (user) or all feedback (admin)

### Admin
- `POST /api/admin/resources` - Create resource
- `PUT /api/admin/resources/{resource_id}` - Update resource
- `DELETE /api/admin/resources/{resource_id}` - Delete resource
- `GET /api/admin/logs` - Get system logs
- `GET /api/admin/analytics` - Get analytics data

## Security Features

- Password hashing with bcrypt
- JWT token authentication
- CORS configuration
- Input validation
- SQL injection protection via ORM
- Crisis keyword detection

## Development

### Running Tests
```bash
cd backend
pytest
```

### Database Migrations
```bash
cd backend
alembic revision --autogenerate -m "Description"
alembic upgrade head
```

## License

MIT License

