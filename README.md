# OpenHW-Studio — Frontend

Cloud Based Hardware & Coding Platform.

## Setup

```bash
npm install
cp .env.example .env
# Fill in your Google Client ID in .env
npm run dev
```

## Google OAuth Setup
1. Go to [Google Cloud Console](https://console.cloud.google.com)
2. Create a project → APIs & Services → Credentials
3. Create OAuth 2.0 Client ID (Web application)
4. Add `http://localhost:5173` to Authorized JavaScript origins
5. Copy the Client ID into your `.env` as `VITE_GOOGLE_CLIENT_ID`

## Folder Structure
```
src/
├── pages/
│   ├── LandingPage.jsx       ← Public homepage (guest access)
│   ├── LoginPage.jsx         ← Google OAuth + role selection
│   ├── RoleSelectPage.jsx    ← Role picker (post-login)
│   ├── StudentDashboard.jsx  ← Protected: students only
│   ├── TeacherDashboard.jsx  ← Protected: teachers only
│   └── SimulatorPage.jsx     ← Guest + logged-in users
├── context/
│   └── AuthContext.jsx       ← Global auth state
├── services/
│   └── authService.js        ← ALL backend API calls (swap URLs when ready)
├── components/
│   └── auth/
│       └── ProtectedRoute.jsx
└── index.css
```

## Backend Integration Checklist
When backend is ready:
- [ ] Set `VITE_API_BASE_URL` in `.env`
- [ ] In `LoginPage.jsx`: Replace `mockLogin()` with real `googleLogin()` call
- [ ] Backend expects: `POST /api/auth/google` → `{ access_token, role }`
- [ ] Backend returns: `{ token: "jwt...", user: { id, name, email, role, points, coins, level } }`

## Routes
| Path | Access | Page |
|------|--------|------|
| `/` | Public | Landing Page |
| `/login` | Public | Login + Role Select |
| `/simulator` | Guest + Logged In | Simulator |
| `/student/dashboard` | Student only | Student Dashboard |
| `/teacher/dashboard` | Teacher only | Teacher Dashboard |
