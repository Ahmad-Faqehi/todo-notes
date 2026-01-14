# Todo Notes

A Flask-based web application for creating, managing, and organizing personal notes with user authentication and database persistence.

## Overview

Todo Notes is a lightweight note-taking application built with Python Flask. It allows users to create an account, securely log in, and manage their personal notes. The application features user authentication, persistent data storage using SQLite, and a responsive web interface.

## Features

- **User Authentication**
  - User registration with email and password
  - Secure login with password hashing (PBKDF2:SHA256)
  - User session management with Flask-Login
  - Remember me functionality

- **Note Management**
  - Create new notes
  - View all personal notes
  - Delete notes with AJAX requests
  - Notes are timestamped and associated with user accounts

- **Database**
  - SQLite database for data persistence
  - User and Note models with relationships
  - Automatic database initialization on app startup

- **Security**
  - Password hashing for user accounts
  - User authentication required for accessing notes
  - CSRF protection through Flask forms

## Tech Stack

- **Backend**: Flask (Python web framework)
- **Database**: SQLite with SQLAlchemy ORM
- **Authentication**: Flask-Login
- **Frontend**: HTML, CSS, JavaScript
- **Containerization**: Docker

## Project Structure

```
.
├── main.py                          # Application entry point
├── requirements.txt                 # Python dependencies
├── Dockerfile                       # Docker configuration
├── README.md                        # This file
├── .github/workflows/
│   └── pipeline.yaml               # CI/CD pipeline configuration
└── website/
    ├── __init__.py                 # Flask app factory and initialization
    ├── auth.py                     # Authentication routes (login, signup, logout)
    ├── models.py                   # Database models (User, Note)
    ├── views.py                    # Main application routes
    ├── static/
    │   └── index.js               # Frontend JavaScript for note management
    └── templates/
        ├── base.html              # Base template with navigation
        ├── home.html              # Home page with note display
        ├── login.html             # Login page
        └── sign_up.html           # User registration page
```

## Installation

### Prerequisites
- Python 3.9+
- pip (Python package manager)

### Local Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/Ahmad-Faqehi/todo-notes.git
   cd todo-notes
   ```

2. **Create a virtual environment**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Run the application**
   ```bash
   python main.py
   ```

   The application will be available at `http://localhost:5000`

### Docker Setup

1. **Build the Docker image**
   ```bash
   docker build -t todo-notes .
   ```

2. **Run the container**
   ```bash
   docker run -p 5000:5000 todo-notes
   ```

## Dependencies

- **flask**: Web application framework
- **Flask-SQLAlchemy**: ORM for database management
- **flask-login**: User authentication and session management

## API Endpoints

### Authentication Routes
- `GET/POST /login` - User login page and authentication
- `GET/POST /sign-up` - User registration
- `GET /logout` - User logout

### Note Routes
- `GET/POST /` - Home page (view and create notes)
- `POST /delete-note` - Delete a note (AJAX endpoint)

## Database Models

### User Model
```python
- id: Integer (Primary Key)
- email: String (Unique)
- password: String (Hashed)
- first_name: String
- notes: Relationship (One-to-Many with Note)
```

### Note Model
```python
- id: Integer (Primary Key)
- data: String (Max 10000 characters)
- date: DateTime (Auto-generated timestamp)
- user_id: Integer (Foreign Key to User)
```

## CI/CD Pipeline

The project uses GitHub Actions for automated CI/CD:
- **Build**: Compiles and tests the application
- **Push**: Pushes Docker image to Docker Hub
- **Deploy**: Deploys to Kubernetes using ArgoCD

**Deploy Conditions**: The deployment stage runs only on branches that don't start with `feature-` (i.e., development, staging, and main branches).

## Configuration

### Flask Configuration
- **SECRET_KEY**: Used for session management (set in `website/__init__.py`)
- **SQLALCHEMY_DATABASE_URI**: SQLite database path
- **Database Name**: `database.db` (automatically created)

**Note**: The SECRET_KEY in the current implementation should be replaced with a secure key in production environments.

## Usage

1. **Create an Account**
   - Navigate to the Sign Up page
   - Enter email, first name, and password
   - Passwords must be at least 7 characters long

2. **Login**
   - Use your registered email and password
   - Enable "Remember Me" for persistent sessions

3. **Create Notes**
   - On the home page, enter note content
   - Notes must contain at least 1 character
   - Click to submit the note

4. **Delete Notes**
   - Click the delete button next to any note
   - Notes are permanently removed from the database

## Security Considerations

- Implement strong password hashing (PBKDF2:SHA256 is used)
- All routes (except login/signup) require authentication
- Use HTTPS in production
- Update SECRET_KEY with a secure value for production
- Consider implementing rate limiting for login attempts
- Use environment variables for sensitive configuration

## Future Enhancements

- Note categories/tags
- Note search functionality
- Note editing capability
- Export notes to PDF/CSV
- Sharing notes with other users
- Dark mode theme
- Mobile app version

## License

This project is open source. Please refer to the LICENSE file for more information.

## Author

Ahmad Faqehi

## Support

For issues, feature requests, or contributions, please open an issue or submit a pull request on GitHub.

