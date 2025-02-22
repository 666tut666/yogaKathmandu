# KATHMANDU YOGA STUDIO DOCUMENTATION

=== PROJECT STRUCTURE ===

-- BACKEND --
backend/
├── app/
│   ├── database.py       # DB configuration
│   ├── models.py         # Data models (User, Course)
│   ├── routes/
│   │   ├── auth.py       # Authentication endpoints
│   │   ├── courses.py    # Course management
│   │   └── contact.py    # Contact forms
├── requirements.txt      # Python dependencies
└── .env.example          # Environment template

-- FRONTEND --
frontend/
├── public/static/images/   # Image assets
├── src/
│   ├── components/         # Reusable UI
│   ├── pages/             # Page components
│   ├── App.js             # Main router
│   └── apiService.js      # API client config

=== SETUP INSTRUCTIONS ===

1. BACKEND SETUP:
```bash
pip install -r requirements.txt
cp .env.example .env  # Update with your credentials
python init_db.py
uvicorn app.main:app --reload
```

2. FRONTEND SETUP:
```bash
cd frontend
npm install
npm start
```

=== API ENDPOINTS ===

[Authentication]
POST /auth/login       - User login (JWT)
POST /auth/register    - New user registration

[Content Management]
GET /courses           - List all courses
POST /testimonials     - Submit new testimonial
GET /users/me          - Get current user profile

=== ENVIRONMENT VARIABLES ===
```ini
# .env file configuration
DATABASE_URL=postgresql://user:password@localhost/yoga_db
JWT_SECRET=your_secure_secret_key_here
ALLOWED_ORIGINS=http://localhost:3000
```

=== CODE EXAMPLES ===

1. User Model (backend/models.py):
```python
class User(Base):
    __tablename__ = "users"
    id = Column(Integer, primary_key=True)
    email = Column(String, unique=True)
    hashed_password = Column(String)
    is_admin = Column(Boolean, default=False)
```

2. API Client (frontend/apiService.js):
```javascript
// Configure request interceptor
API.interceptors.request.use(config => {
  const token = localStorage.getItem('authToken');
  if (token) config.headers.Authorization = `Bearer ${token}`;
  return config;
});
```

=== TROUBLESHOOTING ===

1. Database Connection Issues:
   - Verify PostgreSQL service is running
   - Check .env file values match DB credentials
   - Run: python init_db.py --force

2. Frontend API Errors:
   - Confirm backend server is running
   - Check browser console for CORS errors
   - Validate JWT token in localStorage

3. Dependency Conflicts:
   - Delete venv/ and node_modules/
   - Reinstall using pip/npm commands

=== TESTING ===
```bash
# Backend tests
pytest app/tests/

# Frontend tests
cd frontend && npm test
```
=== VERSION HISTORY ===

2024-02-22 - Repository Migration
- Resolved git push failures due to repository corruption
- Created fresh repository: yogaKathmandu
- Migrated all working files from local copy
- Preserved commit history up to:
  Commit: c428fe986ce6eb0b6c9cb952019d49803c3163bf
  Message: "Properly resolved config file conflicts"

Key Changes:
1. Removed corrupted git objects
2. Reconfigured remote origin
3. Force-pushed valid history
4. Maintained frontend/.gitignore integrity

Lessons Learned:
- Always verify git status before force pushes
- Use --force-with-lease instead of --force
- Regular git fsck checks for repo health