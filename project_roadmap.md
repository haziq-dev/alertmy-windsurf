# AlertMY Project Roadmap

## Project Overview
AlertMY is a comprehensive alert notification system with geospatial capabilities, enabling users to report and receive real-time alerts about various incidents. The system is built with a modern, scalable architecture.

## Technical Stack

### Frontend (alertmy_fe)
- **Framework**: Flutter 3.0+ (Cross-platform: Web, iOS, Android)
- **State Management**: Provider/Riverpod
- **Maps & Location**: Google Maps Flutter, Geolocator
- **Local Storage**: Hive, Shared Preferences
- **Networking**: Dio, http
- **Authentication**: JWT with refresh tokens
- **Push Notifications**: Firebase Cloud Messaging (FCM)

### Backend (alertmy-be)
- **Framework**: Laravel 10.x
- **API**: RESTful with JSON:API specification
- **Authentication**: Laravel Sanctum
- **Database**: PostgreSQL 14+ with PostGIS 3.0+
- **Caching & Queues**: Redis
- **Search**: Laravel Scout with Meilisearch
- **Storage**: Local/S3-compatible storage
- **Admin Panel**: Filament PHP
- **Documentation**: Scribe

### Infrastructure
- **Version Control**: GitHub
- **CI/CD**: GitHub Actions
- **Containerization**: Docker
- **Hosting**: VPS (e.g., DigitalOcean, AWS, GCP)
- **Monitoring**: Laravel Telescope, Sentry

## Project Structure

### Frontend (alertmy_fe)
```
lib/
├── core/               # Core functionality
│   ├── constants/     
│   ├── errors/        
│   ├── services/      
│   └── utils/         
├── features/          # Feature-based modules
│   ├── auth/         
│   ├── alerts/       
│   ├── profile/      
│   └── ...
├── shared/            # Shared widgets and utilities
│   ├── widgets/      
│   ├── theme/        
│   └── localization/ 
└── main.dart         # Application entry point
```

### Backend (alertmy-be)
```
app/
├── Console/          # Artisan commands
├── Http/            
│   ├── Controllers/  # API Controllers
│   ├── Middleware/   
│   └── Requests/     # Form Requests
├── Models/           # Eloquent Models
├── Policies/         # Authorization Policies
└── Services/         # Business Logic

database/
├── factories/       # Model Factories
├── migrations/      # Database Migrations
├── seeders/         # Database Seeders
└── spatial/         # PostGIS specific migrations

routes/
├── api.php         # API Routes
└── web.php         # Web Routes
```

## Development Workflow

### Version Control
- **Branch Naming**: `feature/`, `bugfix/`, `hotfix/`, `release/`
- **Commit Message Convention**: Conventional Commits
- **Code Review**: Required for all PRs
- **CI/CD**: Automated testing and deployment

### Code Quality
- **PHP**: PHP_CodeSniffer, PHPStan
- **Dart**: Flutter Analyze, Dart Analysis
- **Testing**: PHPUnit, Laravel Dusk, Flutter Test
- **Coverage**: Minimum 80% test coverage

## API Design

### Authentication
- JWT-based authentication
- Refresh token mechanism
- Rate limiting (throttling)
- CORS configuration

### Endpoints
- RESTful design
- Versioned API (e.g., `/api/v1/`)
- JSON:API specification
- Pagination, filtering, sorting
- Caching headers

## Database Design

### Key Tables
- `users` - User accounts and authentication
- `alerts` - Alert notifications with geospatial data
- `alert_types` - Categories of alerts
- `confirmations` - User confirmations of alerts
- `devices` - For push notifications
- `notifications` - System notifications

### PostGIS Integration
- Spatial columns for location data
- Geofencing capabilities
- Distance calculations
- Spatial indexing for performance

## Security

### Authentication & Authorization
- JWT token-based authentication
- Role-based access control (RBAC)
- OAuth2 for third-party integrations
- CSRF protection

### Data Protection
- Input validation and sanitization
- SQL injection prevention
- XSS protection
- Rate limiting
- API key authentication for public endpoints

## Deployment Strategy

### Environments
1. **Development** - Local development
2. **Staging** - Pre-production testing
3. **Production** - Live environment

### Infrastructure as Code
- Docker Compose for local development
- Terraform for infrastructure provisioning
- Ansible for configuration management

### CI/CD Pipeline
1. Code push triggers build
2. Run tests and code analysis
3. Build artifacts
4. Deploy to staging/production
5. Run migrations
6. Clear caches

## Monitoring & Maintenance

### Logging
- Structured logging with context
- Log rotation and retention
- Centralized log management

### Performance Monitoring
- Application performance monitoring (APM)
- Database query optimization
- Cache hit/miss ratios

### Alerting
- Error tracking (Sentry)
- Uptime monitoring
- Performance alerts

## Future Enhancements

### Short-term
- [ ] User profile management
- [ ] Advanced alert filtering
- [ ] Offline support
- [ ] Push notifications

### Medium-term
- [ ] Real-time updates with WebSockets
- [ ] AI-based alert verification
- [ ] User reputation system
- [ ] Multi-language support

### Long-term
- [ ] Machine learning for alert prediction
- [ ] Integration with government APIs
- [ ] Mobile wallet integration for rewards
- [ ] IoT device integration

## Success Metrics

### Key Performance Indicators (KPIs)
- System uptime (target: 99.9%)
- API response time (p95 < 500ms)
- User growth rate
- Alert resolution time
- User engagement metrics

## Team & Responsibilities

### Development Team
- **Frontend Developers**: 2-3
- **Backend Developers**: 2
- **DevOps Engineer**: 1
- **QA Engineer**: 1
- **Product Manager**: 1

### Communication
- Daily stand-ups
- Bi-weekly sprint planning
- Weekly demos
- Monthly retrospectives

## Timeline

### Phase 1: Foundation (Weeks 1-4)
- Project setup and architecture
- Core features development
- Basic testing infrastructure

### Phase 2: Core Features (Weeks 5-8)
- User authentication
- Alert creation and management
- Basic admin panel

### Phase 3: Enhanced Features (Weeks 9-12)
- Real-time updates
- Advanced search and filtering
- Push notifications

### Phase 4: Polish & Launch (Weeks 13-16)
- Performance optimization
- Security audit
- Beta testing
- Production deployment

## Risk Management

### Identified Risks
1. **Technical Risks**
   - Performance bottlenecks
   - Third-party service dependencies
   - Data consistency issues

2. **Project Risks**
   - Scope creep
   - Resource constraints
   - Timeline delays

### Mitigation Strategies
- Regular code reviews
- Automated testing
- Feature flags
- Rollback procedures
- Regular backups

## Budget

### Development Costs
- Development team salaries
- Infrastructure costs
- Third-party services
- Tools and licenses

### Operational Costs
- Hosting
- Storage
- Bandwidth
- Support and maintenance

## Legal & Compliance

### Data Protection
- GDPR compliance
- Data retention policy
- User data export/delete

### Terms of Service
- Acceptable use policy
- Liability limitations
- Intellectual property rights

## Conclusion
This roadmap provides a comprehensive guide for the development and maintenance of the AlertMY platform. It will be regularly updated to reflect changes in requirements, technology, or business priorities.

---

## Phase 1: Environment Setup

### 1. Install Prerequisites
**Goal:** Prepare a full local development environment.

- **Windows:** Ensure WSL2 with Ubuntu is installed and configured.
- **Database:** Install PostgreSQL and enable PostGIS extension inside WSL2.
- **PHP & Composer:** Install latest PHP version (≥ 8.3) and Composer.
- **Laravel:** Use Laravel 11 with Breeze for starter auth or install Filament directly.
- **Node.js:** Required for frontend builds within Laravel (e.g., Breeze or Filament).
- **Flutter SDK:** Install via stable channel; ensure Android Studio SDK and emulator are working.

### 2. Configure PostgreSQL (WSL2)
**Goal:** Host PostgreSQL locally via WSL2 and connect Laravel.

- Create a dedicated PostgreSQL user and database for AlertMY.
- Enable PostGIS with `CREATE EXTENSION postgis;`.
- Confirm that Laravel can connect via `.env` using local IP or socket path.

### 3. Folder Structure
**Goal:** Keep backend and mobile in a single workspace.

```
alertmy/
├── backend/ (Laravel)
├── mobile/ (Flutter)
└── docs/ (Documentation)
```

---

## Phase 2: Backend (Laravel API)

### 1. API-First Architecture
**Goal:** Laravel will serve as a headless REST API consumed by Flutter.

- Use Laravel routes under `/api` for all mobile interactions.
- Use Sanctum or JWT for user authentication tokens.
- Avoid Blade views for mobile endpoints — use Filament for admin.

### 2. Database Design
**Goal:** Use spatial data to locate alerts.

Tables:
- **alerts** — stores reports with category, description, photo, and geolocation.
- **confirmations** — stores user confirmations to validate alerts.
- **users** — standard Laravel users, integrated with Google login.

Add PostGIS column types (e.g., `geography(Point, 4326)`) for location.

### 3. Google Login (Laravel Socialite)
**Goal:** Enable Google sign-in for mobile app users.

- Use Socialite for OAuth 2.0 authentication.
- On successful login, issue a Laravel Sanctum token to Flutter.
- Store user profiles with name, email, and avatar for later use in Filament.

### 4. Storage Handling
**Goal:** Manage alert photo uploads.

- Use Laravel’s Storage facade to store files locally during development.
- Configure S3-compatible storage for production (e.g., DigitalOcean Spaces).
- Return accessible URLs to Flutter for each uploaded image.

### 5. API Documentation
**Goal:** Maintain clean API reference.

- Document endpoints in `/docs/api.md` or use Postman collections.
- Clearly define routes for: `auth`, `alerts`, and `confirmations`.

---

## Phase 3: Admin Dashboard (Laravel Filament)

### 1. Setup Filament
**Goal:** Provide CMS interface for admins.

- Install Filament inside Laravel backend.
- Use roles/permissions (e.g., Spatie) to restrict access.
- Create panels for:
  - Managing users
  - Viewing alerts with maps
  - Reviewing confirmation activity

### 2. Integrate Maps in Filament
**Goal:** Display alert locations visually.

- Use Filament forms with custom Leaflet or Mapbox field.
- Query data using PostGIS for proximity or clustering.

### 3. Dashboard Features
**Goal:** Allow monitoring and moderation.

- Filter alerts by category, date, or region.
- Approve or delete invalid reports.
- View total users and alert distribution metrics.

---

## Phase 4: Flutter App

### 1. Project Setup
**Goal:** Initialize Flutter app to consume Laravel API.

- Use `flutter create mobile` inside the workspace.
- Organize folders as `screens`, `services`, `models`, and `widgets`.
- Configure environment variables for API base URLs.

### 2. Authentication
**Goal:** Support Google sign-in and Laravel token sync.

- Use `google_sign_in` package for mobile-side login.
- Send user’s Google token to Laravel endpoint for validation and token generation.

### 3. Location + Map
**Goal:** Display nearby alerts.

- Use `geolocator` to get user’s current position.
- Display map using `flutter_map` or `google_maps_flutter`.
- Fetch nearby alerts via Laravel endpoint using PostGIS `ST_DWithin` query.

### 4. Alert Creation
**Goal:** Allow users to post new alerts.

- Simple form: category, description, optional photo.
- Capture GPS location automatically.
- Upload photo via multipart to Laravel API.

### 5. Alert Confirmation
**Goal:** Allow users to validate alerts.

- Tap alert to confirm it’s still valid.
- Laravel updates `confirmed_count` and prevents duplicate confirmations.

### 6. Notifications
**Goal:** Real-time alert updates.

- Use Firebase Cloud Messaging (FCM) for push notifications.
- Laravel sends notifications when a new alert is within proximity.

---

## Phase 5: Deployment

### 1. Backend Deployment
**Goal:** Deploy Laravel + PostgreSQL.

- Use a VPS (Ubuntu) or managed Laravel host.
- Install PostgreSQL + PostGIS.
- Setup Nginx and SSL with Certbot.
- Point `.env` variables to production database and storage.

### 2. Flutter App Deployment
**Goal:** Build and release app to Play Store.

- Configure app name, icon, and splash screen.
- Build APK or App Bundle.
- Upload via Play Console with privacy policy.

---

## Phase 6: Future Enhancements

- User-level trust scores based on confirmation accuracy.
- AI-based incident classification (optional future goal).
- Community moderation and reward system.
- Offline caching and sync for poor connectivity.

---

## Summary
By following this roadmap, you’ll have:
1. **A robust Laravel API** with spatial data support and Google login.
2. **A Flutter mobile app** for Android that reports and views real-time alerts.
3. **An admin dashboard via Filament** for management and monitoring.
4. **A scalable, modern architecture** ready for deployment to production.