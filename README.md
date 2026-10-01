# Job Board Platform - Django REST Framework Backend

![Django](https://img.shields.io/badge/Django-4.2-green)
![DRF](https://img.shields.io/badge/DRF-3.14-blue)
![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![License](https://img.shields.io/badge/License-MIT-green)

A complete, production-ready backend for a modern job board platform built with Django and Django REST Framework. Includes JWT authentication, job management, resume uploads, and application tracking.

## 🎯 Features

### ✅ Core Features

- **User Management**
  - Custom user model with multiple roles (Employer, Candidate, Admin)
  - JWT authentication with simplejwt
  - Email verification
  - Profile management

- **Employer Features**
  - Create and manage job listings
  - Track applications for posted jobs
  - View candidate profiles
  - Company profile management with logo
  - Job posting status management

- **Candidate Features**
  - Browse and search jobs with advanced filters
  - Upload and manage multiple resumes
  - Apply for jobs with cover letters
  - Track application status
  - Build candidate profile with skills and experience

- **Job Management**
  - Full CRUD operations for job listings
  - Advanced filtering (type, location, remote, experience level)
  - Salary range tracking
  - Job expiration management
  - View count tracking
  - Rich job descriptions and requirements

- **Applications**
  - Submit job applications
  - Track application status (Pending → Reviewed → Interviewing → Accepted/Rejected)
  - Rating system for candidates
  - Internal notes for employers
  - Application withdrawal

- **Admin Panel**
  - Comprehensive Django admin interface
  - User management with role filtering
  - Job and application management
  - Resume management
  - Employer verification
  - Custom admin actions

### 🔒 Security Features

- JWT Token-based authentication
- Role-based access control (RBAC)
- CORS support
- Rate limiting
- File upload validation
- Input validation and sanitization

### 📊 API Features

- RESTful API with proper HTTP methods
- Pagination for list endpoints
- Advanced filtering and search
- Multiple serializers for different use cases
- Comprehensive error handling
- OpenAPI documentation ready

### 📱 File Management

- Resume upload (PDF, DOC, DOCX)
- Company logo upload
- Profile picture upload
- File size validation
- File type validation

---

## 🚀 Quick Start

### Prerequisites

- Python 3.8 or higher
- pip (Python package manager)
- Virtual environment tool (venv)

### Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/yourusername/job-board-backend.git
   cd job-board-backend
   ```

2. **Create and activate virtual environment:**
   ```bash
   python3 -m venv venv
   source venv/bin/activate  # macOS/Linux
   # or
   venv\Scripts\activate  # Windows
   ```

3. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Set up environment variables:**
   ```bash
   cp .env.example .env
   # Edit .env with your configuration
   ```

5. **Run migrations:**
   ```bash
   python manage.py makemigrations
   python manage.py migrate
   ```

6. **Create superuser:**
   ```bash
   python manage.py createsuperuser
   ```

7. **Run development server:**
   ```bash
   python manage.py runserver
   ```

Access the API at: `http://localhost:8000/api/`
Access admin at: `http://localhost:8000/admin/`

---

## 📚 API Endpoints

### Authentication
- `POST /api/auth/register/` - Register as candidate
- `POST /api/auth/register-employer/` - Register as employer
- `POST /api/auth/token/` - Get JWT tokens
- `POST /api/auth/token/refresh/` - Refresh access token

### Jobs
- `GET /api/jobs/` - List all jobs (with filters)
- `POST /api/jobs/` - Create job (employer)
- `GET /api/jobs/{id}/` - Get job details
- `PUT /api/jobs/{id}/` - Update job (employer)
- `DELETE /api/jobs/{id}/` - Delete job (employer)
- `GET /api/jobs/search/` - Advanced search

### Applications
- `GET /api/applications/` - List applications
- `POST /api/applications/` - Submit application (candidate)
- `GET /api/applications/{id}/` - Get application details
- `PATCH /api/applications/{id}/` - Update status (employer)
- `POST /api/applications/{id}/withdraw/` - Withdraw application

### Resumes
- `GET /api/resumes/` - List resumes
- `POST /api/resumes/` - Upload resume (candidate)
- `DELETE /api/resumes/{id}/` - Delete resume
- `POST /api/resumes/{id}/set_primary/` - Set as primary

### Profiles
- `GET /api/users/profile/` - Get user profile
- `PUT /api/users/profile/` - Update user profile
- `GET /api/employers/` - List employers
- `GET /api/employers/my_profile/` - Get employer's profile
- `GET /api/candidates/my_profile/` - Get candidate's profile

### Dashboard
- `GET /api/dashboard/stats/` - Get dashboard statistics

For complete API documentation, see [API_DOCUMENTATION.md](./API_DOCUMENTATION.md)

---

## 📁 Project Structure

```
job_board_project/
├── job_board/                  # Django project settings
│   ├── settings.py             # Main settings
│   ├── urls.py                 # Project URLs
│   ├── asgi.py
│   └── wsgi.py
├── jobs/                       # Main application
│   ├── models.py              # Database models
│   ├── serializers.py         # DRF serializers
│   ├── views.py               # API views
│   ├── urls.py                # App URLs
│   ├── permissions.py         # Custom permissions
│   ├── admin.py               # Admin configuration
│   └── migrations/            # Database migrations
├── media/                      # User uploads
├── staticfiles/                # Static files
├── logs/                       # Application logs
├── requirements.txt            # Dependencies
├── .env.example               # Example environment
├── manage.py                  # Django CLI
├── SETUP_GUIDE.md            # Detailed setup guide
├── API_DOCUMENTATION.md      # API reference
└── README.md                 # This file
```

---

## 🔧 Configuration

### Environment Variables

Key environment variables (see `.env.example` for all):

```env
# Django
DEBUG=True
DJANGO_SECRET_KEY=your-secret-key
ALLOWED_HOSTS=localhost,127.0.0.1

# Database (SQLite for dev, PostgreSQL for prod)
DB_ENGINE=django.db.backends.sqlite3

# CORS
CORS_ALLOWED_ORIGINS=http://localhost:3000

# JWT
JWT_ALGORITHM=HS256
```

### Settings.py Configuration

Key settings in `settings.py`:

```python
# REST Framework
REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': (
        'rest_framework_simplejwt.authentication.JWTAuthentication',
    ),
    'DEFAULT_PAGINATION_CLASS': 'rest_framework.pagination.PageNumberPagination',
    'PAGE_SIZE': 10,
}

# JWT
SIMPLE_JWT = {
    'ACCESS_TOKEN_LIFETIME': timedelta(minutes=60),
    'REFRESH_TOKEN_LIFETIME': timedelta(days=1),
}

# Custom User Model
AUTH_USER_MODEL = 'users.CustomUser'
```

---

## 🧪 Testing

### Running Tests

```bash
# Run all tests
python manage.py test

# Run specific app tests
python manage.py test jobs

# Run with coverage
pytest --cov=jobs
```

### Testing Endpoints with cURL

```bash
# Register
curl -X POST http://localhost:8000/api/auth/register/ \
  -H "Content-Type: application/json" \
  -d '{"email":"test@example.com","username":"test","password":"pass123"}'

# Login
curl -X POST http://localhost:8000/api/auth/token/ \
  -H "Content-Type: application/json" \
  -d '{"email":"test@example.com","password":"pass123"}'

# Get profile (with token)
curl -H "Authorization: Bearer YOUR_TOKEN" \
  http://localhost:8000/api/users/profile/
```

### Testing with Postman

1. Import collection from endpoints documentation
2. Set up environment variables:
   - `base_url`: `http://localhost:8000/api`
   - `access_token`: JWT token from login
3. Run requests using Bearer token authentication

---

## 🗄️ Database Models

### CustomUser
- Extends Django's AbstractUser
- Multiple roles: employer, candidate, admin
- Email verification tracking
- Profile picture support

### EmployerProfile
- Company information
- Verification status
- Logo upload
- Company metadata

### CandidateProfile
- Bio and skills
- Experience tracking
- Social profiles (LinkedIn, GitHub, portfolio)
- Job search preferences

### JobListing
- Full job description
- Salary range
- Remote/location flexibility
- Experience level
- Status management

### Resume
- PDF/DOC/DOCX upload
- Primary resume designation
- File size tracking

### JobApplication
- Application status tracking
- Cover letter
- Candidate rating
- Employer notes

---

## 🔐 Authentication & Permissions

### JWT Authentication

1. **Register** → Get user account
2. **Login** → Get access + refresh tokens
3. **Use Access Token** → Include in `Authorization: Bearer <token>` header

### Role-Based Permissions

- **Public**: Register, Login, List Jobs
- **Candidate**: Search jobs, Apply, Upload resume, Track applications
- **Employer**: Post jobs, View applications, Rate candidates
- **Admin**: Full access to all models

### Custom Permission Classes

```python
IsEmployer      # Only employers
IsCandidate     # Only candidates
IsOwner         # Owner of resource
IsJobOwner      # Employer who posted job
IsReadOnlyOrEmployer  # Read all, write as employer
```

---

## 📧 Signals & Notifications

Automatic triggers for:

- New job application → Notify employer
- Application status change → Notify candidate
- New job posting → Notification system ready
- User profile creation → Auto-create candidate profile

Implement email notifications by connecting signal handlers.

---

## 🚢 Deployment

### Using Heroku

```bash
heroku login
heroku create your-app-name
heroku config:set DEBUG=False
heroku config:set DJANGO_SECRET_KEY=your-key
heroku addons:create heroku-postgresql:hobby-dev
git push heroku main
heroku run python manage.py migrate
```

### Using Docker

```bash
docker-compose up
```

See [SETUP_GUIDE.md](./SETUP_GUIDE.md) for detailed deployment instructions.

---

## 📊 Admin Panel

Access at `/admin/` with superuser credentials:

- **Users**: View/filter by role, verify emails
- **Jobs**: Manage postings, view applications
- **Applications**: Update status, rate candidates
- **Resumes**: Download and verify files
- **Employers**: Verify company profiles

Custom admin features:
- Color-coded role badges
- Application status with colors
- Resume file preview
- Company logo preview
- Quick actions for common tasks

---

## 🔄 Database Migrations

```bash
# Create migrations
python manage.py makemigrations

# View migration status
python manage.py showmigrations

# Apply migrations
python manage.py migrate

# Revert migrations
python manage.py migrate jobs 0001  # Revert to specific migration
```

---

## 📝 Code Quality

### Code Style

- PEP 8 compliant
- Black formatting ready
- Flake8 compatible

```bash
# Check code style
flake8 jobs/

# Format code
black jobs/

# Sort imports
isort jobs/
```

### Logging

Configured logging for:
- Django operations
- Application events
- API requests/responses
- Database operations

View logs at: `logs/job_board.log`

---

## 🐛 Troubleshooting

### Common Issues

**Issue: Database Locked**
```bash
rm db.sqlite3
python manage.py migrate
```

**Issue: CORS Errors**
- Update `CORS_ALLOWED_ORIGINS` in `.env`

**Issue: Token Expired**
- Use refresh token at `/api/auth/token/refresh/`

**Issue: File Upload Fails**
- Check file size (max 5MB)
- Check file type (pdf, doc, docx only)
- Check media directory permissions

See [SETUP_GUIDE.md](./SETUP_GUIDE.md#troubleshooting) for more solutions.

---

## 📚 Documentation

- [SETUP_GUIDE.md](./SETUP_GUIDE.md) - Detailed installation and setup
- [API_DOCUMENTATION.md](./API_DOCUMENTATION.md) - Complete API reference
- [Django Docs](https://docs.djangoproject.com/)
- [DRF Docs](https://www.django-rest-framework.org/)

---

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## 📄 License

This project is licensed under the MIT License - see LICENSE file for details.

---

## 👨‍💻 Authors

**CodeAlpha Internship Project - Task 4**
- Backend Architecture & Implementation
- Django/DRF Best Practices
- Production-Ready Code

---

## 🙏 Acknowledgments

- Django Framework
- Django REST Framework
- Simple JWT
- Django Filter
- All contributors and supporters

---

## 📞 Support

For issues, questions, or suggestions:
1. Check the [SETUP_GUIDE.md](./SETUP_GUIDE.md#troubleshooting)
2. Review [API_DOCUMENTATION.md](./API_DOCUMENTATION.md)
3. Open an issue on GitHub
4. Contact the development team

---

## 🗺️ Roadmap

### Upcoming Features
- [ ] Email notifications
- [ ] Advanced analytics
- [ ] Interview scheduling
- [ ] Skills endorsement system
- [ ] Advanced recommendation engine
- [ ] Integration with ATS systems
- [ ] Mobile app support
- [ ] Video interview integration
- [ ] Salary insights and analytics
- [ ] Job recommendation ML model

### Infrastructure
- [ ] Full API documentation with Swagger
- [ ] Automated testing pipeline
- [ ] Performance optimization
- [ ] Caching layer (Redis)
- [ ] Message queue (Celery)
- [ ] Monitoring and alerting

---

**Version:** 1.0.0  
**Last Updated:** January 2024  
**Status:** Production Ready ✅

---

