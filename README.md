# Angular 21 Auth Boilerplate (Beginner Guide)

This project is a beginner-friendly Angular 21 boilerplate that demonstrates a complete authentication flow:

- Email sign up + email verification
- Login + logout
- JWT auth header for API requests
- Refresh tokens (cookie-based) + auto-refresh before access token expiry
- Forgot password + reset password
- Role-based authorization (User & Admin)
- Admin area for account management
 - Profile area for viewing/updating your own account

 ## Table of contents

 - [1) Prerequisits](#1-prerequisits)
 - [2) Run the app (real API)](#2-run-the-app-real-api)
 - [3) Run the app (fake backend, no API)](#3-run-the-app-fake-backend-no-api)
 - [4) Using the app (what to click)](#4-using-the-app-what-to-click)
 - [5) How authenticate works](#5-ow-authenticate-works)
 - [6) Authorization (roles + route guards)](#6-authorization-roles--route-guards)
 - [7) Project structure (quick tour)](#7-project-structure-quick-tour)
  - [8) Troubleshooting](#8-troubleshooting)

  ## 1) Prerequisits

  - Node.js (LTS recommended)
  - npm (cones with Node.js)