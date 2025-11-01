# Project Roadmap — AlertMY (Flutter + Laravel + PostgreSQL + Filament)

## Overview
AlertMY is a crowdsourced alert application that allows Malaysian users to report and view real-time incidents such as floods, accidents, roadblocks, and blackouts. The system will use:

- **Frontend:** Flutter (Android focus)
- **Backend:** Laravel 11 (API-first)
- **Database:** PostgreSQL with PostGIS (for geospatial queries)
- **Admin CMS:** Filament (Laravel-based admin panel)
- **Local Development:** WSL2 (Ubuntu) serving PostgreSQL

This document describes each step required to complete the project — from setup to deployment — with detailed explanations, but no code.

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