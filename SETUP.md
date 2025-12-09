# Setup Instructions

## Prerequisites

1. **Python 3.9+** - [Download Python](https://www.python.org/downloads/)
2. **PostgreSQL 12+** - [Download PostgreSQL](https://www.postgresql.org/download/)
3. **pip** - Usually comes with Python

## Step 1: Database Setup

1. Install PostgreSQL and start the service
2. Create a database:
   ```sql
   CREATE DATABASE mentalhealth_db;
   ```
3. Note your database connection details (username, password, host, port)

## Step 2: Backend Setup

1. Navigate to the backend directory:
   ```bash
   cd backend
   ```

2. Create a virtual environment:
   ```bash
   # Windows
   python -m venv venv
   venv\Scripts\activate

   # Linux/Mac
   python3 -m venv venv
   source venv/bin/activate
   ```

3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

4. Create a `.env` file in the `backend` directory:
   ```env
   DATABASE_URL=postgresql://username:password@localhost:5432/mentalhealth_db
   SECRET_KEY=your-super-secret-key-change-this-in-production-min-32-chars
   ALGORITHM=HS256
   ACCESS_TOKEN_EXPIRE_MINUTES=30
   ENVIRONMENT=development
   ```
   
   Replace `username`, `password`, and `localhost:5432` with your PostgreSQL credentials.

5. Initialize the database:
   ```bash
   python database/init_db.py
   ```

6. Seed initial data:
   ```bash
   python seed_data.py
   ```

7. Start the backend server:
   ```bash
   uvicorn main:app --reload --host 0.0.0.0 --port 8000
   ```

   The API will be available at:
   - API: `http://localhost:8000`
   - Docs: `http://localhost:8000/docs`
   - Redoc: `http://localhost:8000/redoc`

## Step 3: Frontend Setup

1. Navigate to the frontend directory:
   ```bash
   cd frontend
   ```

2. Open `index.html` in a web browser, or use a local server:

   **Option 1: Using Python's HTTP server**
   ```bash
   # Python 3
   python -m http.server 8080
   
   # Then open http://localhost:8080 in your browser
   ```

   **Option 2: Using Node.js http-server**
   ```bash
   npx http-server -p 8080
   ```

   **Option 3: Using VS Code Live Server extension**
   - Install the "Live Server" extension
   - Right-click on `index.html` and select "Open with Live Server"

3. If using a different port, update `API_BASE_URL` in `frontend/js/config.js`

## Test Accounts

After seeding the database, you can use these accounts:

### Regular User
- **Email**: `user@test.com`
- **Password**: `123456`

### Admin User
- **Email**: `admin@test.com`
- **Password**: `admin123`

## Troubleshooting

### Database Connection Issues
- Ensure PostgreSQL is running
- Check that the database exists
- Verify credentials in `.env` file
- Test connection: `psql -U username -d mentalhealth_db`

### Import Errors
- Ensure virtual environment is activated
- Reinstall dependencies: `pip install -r requirements.txt --force-reinstall`
- Check Python path

### CORS Issues
- Ensure backend is running on port 8000
- Check `API_BASE_URL` in `frontend/js/config.js`
- Verify CORS settings in `backend/main.py`

### Port Already in Use
- Change backend port: `uvicorn main:app --reload --port 8001`
- Update `API_BASE_URL` in frontend config
- Or kill the process using the port

## Development

### Running Tests
```bash
cd backend
pytest
```

### Database Migrations
This project uses SQLAlchemy's automatic table creation. For production, consider using Alembic for migrations:
```bash
alembic revision --autogenerate -m "Description"
alembic upgrade head
```

### Production Deployment
1. Set strong `SECRET_KEY` in `.env`
2. Use environment-specific `DATABASE_URL`
3. Enable HTTPS
4. Configure proper CORS origins
5. Use production WSGI server (e.g., Gunicorn)
6. Set up reverse proxy (Nginx)

## API Endpoints

See the interactive API documentation at `http://localhost:8000/docs` after starting the backend.

## Project Structure

```
├── backend/
│   ├── api/           # API routes
│   ├── auth/          # Authentication
│   ├── database/      # Database configuration
│   ├── models/        # SQLAlchemy models
│   ├── schemas/       # Pydantic schemas
│   ├── services/      # Business logic
│   ├── main.py        # FastAPI app
│   └── seed_data.py   # Database seeding
├── frontend/
│   ├── js/            # JavaScript modules
│   ├── styles/        # CSS files
│   └── index.html     # Main HTML file
└── README.md

```

