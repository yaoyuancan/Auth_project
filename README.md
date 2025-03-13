# Secure Authentication System

A robust authentication system implementing multiple authentication strategies with role-based access control and comprehensive security features.

## Features

- Local authentication (email/password)
- Social authentication (Google)
- JWT-based session management
- Email verification system
- Password reset functionality
- Role-based access control
- Protection against XSS/CSRF attacks
- Rate limiting
- Input validation

## Prerequisites

- Node.js
- MongoDB
- Gmail account (for email notifications)
- Google OAuth credentials

## Setup Instructions

1. Clone the repository:
```bash
git clone https://github.com/yaoyuancan/Auth_project.git
cd https-project2
```

2. Install dependencies:
```bash
npm install
```

3. Create `.env` file in the root directory with the following variables:
```env
# Server Configuration
PORT=3000                  # Application port
NODE_ENV=development      # Environment (development/production)

# Database
MONGODB_URL=mongodb://127.0.0.1:27017/https-project

# Security
JWT_SECRET=your_jwt_secret_here    # Random string for JWT signing

# Google OAuth (Required for Google Login)
# Get these credentials from Google Cloud Console: https://console.cloud.google.com
GOOGLE_CLIENT_ID=your_google_client_id_here         # e.g., xxx.apps.googleusercontent.com
GOOGLE_CLIENT_SECRET=your_google_client_secret_here # Keep this secret!
GOOGLE_REDIRECT_URL=https://localhost:3000/auth/google/callback
```

> **Important**: Never commit the actual `.env` file to version control. The above is just a template.
> Replace the placeholder values with your actual credentials.

4. Start the server:
```bash
npm start
```

The server will run on `https://localhost:3000` by default.

## Authentication Mechanisms

### Local Authentication
- Uses email/password combination
- Passwords are hashed using bcrypt before storage
- JWT tokens issued upon successful authentication
- Tokens expire after 24 hours

### Social Authentication
- Supports Google and Facebook OAuth 2.0
- Implemented using Passport.js strategies
- Creates unified user profiles across authentication methods

### Session Management
- JWT-based stateless authentication
- Secure HTTP-only cookies
- CSRF token validation for protected routes
- Rate limiting on authentication endpoints

## Role-Based Access Control

### User Roles
1. **Regular User**
   - Access to public blogs
   - Basic application features

2. **Admin**
   - Content management
   - Access to admin dashboard

### Permission System
- Role-based middleware
- Route protection based on user roles

## Security Features

- HTTPS/SSL encryption
- Input validation using express-validator
- XSS protection through content sanitization
- CSRF protection using tokens

## Lessons Learned

1. **Password Security**
   - Implemented strong hashing (bcrypt)
   - Secure storage mitigated data breach risks

2. **Token Management**
   - HttpOnly cookies prevented XSS attacks
   - Refresh tokens improved user experience

3. **Role Enforcement**
   - Middleware-based role permissions
   - Simplified control over protected routes

4. **SSO Implementation**
   - Careful handling of Google OAuth tokens
   - Enhanced user accessibility

5. **Session Security**
   - CSRF protection implementation
   - Session fixation prevention strategies

### Challenges Faced
1. **OAuth Integration**
   - Challenge: Handling various OAuth provider responses

2. **Session Management**
   - Challenge: Secure token handling
   - Solution: HTTP-only cookies with JWT
