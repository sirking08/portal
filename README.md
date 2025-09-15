# Javierada System Documentation

## Table of Contents
1. [System Overview](#system-overview)
2. [Architecture](#architecture)
3. [Data Flow](#data-flow)
4. [Data Handling Process](#data-handling-process)
5. [Security Measures](#security-measures)
6. [Authentication & Authorization](#authentication--authorization)
7. [Email System](#email-system)
8. [File Handling](#file-handling)
9. [Deployment](#deployment)
10. [Troubleshooting](#troubleshooting)

## System Overview

Javierada is a web-based transaction management system designed for handling various types of transactions including donations, payments, and other financial operations. The system is built with Ruby on Rails 8 and follows modern web development practices.

**Key Features:**
- User authentication and authorization
- Transaction management
- File uploads and storage
- Email notifications
- Admin dashboard
- Reporting and analytics
- Multi-role access control

## Architecture

### Technology Stack
- **Backend**: Ruby on Rails 8
- **Frontend**: HTML5, CSS3, JavaScript, Bootstrap 5
- **Database**: PostgreSQL
- **File Storage**: Active Storage with Disk/Cloud Storage
- **Background Jobs**: SolidQueue (default), Active Job
- **Authentication**: Devise with OmniAuth (Google, Facebook)
- **Deployment**: Capistrano with Kamal
- **Web Server**: Puma
- **Reverse Proxy**: Nginx

### Directory Structure
```
app/
├── assets/           # Frontend assets
├── controllers/      # Application controllers
├── mailers/          # Email templates and logic
├── models/           # Database models
├── policies/         # Pundit policies for authorization
├── services/         # Business logic
└── views/            # View templates
```

## Data Flow

### User Authentication Flow
1. User visits the application
2. Can sign up/in via:
   - Email/password
   - Google OAuth
   - Facebook OAuth
3. Session is established and maintained via cookies
4. Role-based access control enforces permissions

### Transaction Flow
1. User submits a transaction with required details
2. System validates and processes the transaction
3. File uploads are handled via Active Storage
4. Background jobs process email notifications
5. Admin/Manager reviews and updates transaction status
6. User receives status updates via email

## Data Handling Process

### Transaction Processing
1. **Creation**:
   - User fills out transaction form
   - System validates input
   - Files are uploaded and processed
   - Transaction record is created
   - Confirmation email is queued

2. **Status Updates**:
   - Pending → Confirmed/Cancelled → (optionally) Refunded
   - Each status change triggers appropriate notifications
   - Audit trail is maintained

### File Handling
- Files are stored using Active Storage
- Direct uploads to cloud storage (configurable)
- File type and size validation
- Virus scanning (if configured)
- Secure file serving with signed URLs

## Security Measures

### Authentication
- Secure password hashing with bcrypt
- OAuth 2.0 for third-party authentication
- Account lockout after failed attempts
- Email confirmation required
- Password complexity requirements

### Authorization
- Role-based access control (Admin, Manager, User)
- Pundit for fine-grained authorization
- Policy objects for complex permission logic
- CSRF protection
- CORS configuration

### Data Protection
- Encrypted credentials for sensitive data
- Database encryption for PII
- Secure session handling
- Rate limiting on authentication endpoints
- SQL injection prevention
- XSS protection

## Authentication & Authorization

### User Roles
1. **Admin**: Full system access
2. **Manager**: Transaction management, reporting
3. **User**: Basic access, transaction submission

### OAuth Configuration
- Google OAuth 2.0
- Facebook OAuth 2.0
- Configurable through admin interface

## Email System

### Email Templates
- Transaction confirmation
- Status updates
- Password reset
- Account confirmation

### Configuration
- SMTP settings configurable via admin interface
- Environment variables for sensitive data
- Support for multiple environments

## File Handling

### Storage
- Local disk (development)
- Cloud storage (production)
- Secure file serving

### Security
- File type validation
- Size limits
- Virus scanning (if configured)
- Access control

## Deployment

### Infrastructure
- Ubuntu server
- Nginx as reverse proxy
- PostgreSQL database
- Redis for caching (if configured)

### Deployment Process
1. Code pushed to repository
2. CI/CD pipeline runs tests
3. Automated deployment with Kamal
4. Database migrations
5. Asset precompilation
6. Service restart

## Troubleshooting

### Common Issues
1. **Login Issues**:
   - Check session configuration
   - Verify OAuth credentials
   - Check user account status

2. **Email Delivery**:
   - Verify SMTP settings
   - Check spam folder
   - Review mail server logs

3. **File Uploads**:
   - Check storage permissions
   - Verify file size limits
   - Check storage configuration

### Logs
- Application logs: `log/production.log`
- Web server logs: `/var/log/nginx/`
- Database logs: Check PostgreSQL logs

## Monitoring
- Error tracking with Sentry (if configured)
- Performance monitoring
- Uptime monitoring

## Backup & Recovery
- Regular database backups
- File storage backups
- Disaster recovery plan

---
*Documentation last updated: September 15, 2025*
