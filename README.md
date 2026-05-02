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
  - (Optional) Angular CLI:
    - `npm i -g @angular/cli`

## 2) Run the app (real API)

By default this project is set up to call a real API at:

- `http://localhost:4000` (see `src/environments/environment.ts`)

### Setp 1: Install packages

from the project root (where `package.json` is):

```bash
npm install
```

### Step 2: start your backend API

Start an API that implements the `/accounts/*` endpoints described in the [How authentication works](#5-how-authentication-works) section.

The frontend expects the API to be available at `http://localhost:4000` by default.

### Step 3: start Angular

```bash
npm start
```

This runs `ng serve --open` and should open the app in your browser.

#### Step 4: update API URL (if your API runs elsewhere)

Edit the environment file:

- `src/environments/environment.ts` (development)
- `src/environments/environment.prod.ts` (production build)

Update:

```ts
apiURL: 'http://localhost:4000'
```

## 3) Run the app (fake backend, no API)

If you want to run everything full in the browser (no backend), you can enable the built-in fake backend interceptor.

### Step 1: enable the fake backend provider

Open `src/app/app.module.ts` and uncomment the `fakeBackendProvider` line in the `providers` array.

It should look like this:

```ts
   providers: [
        { provide: APP_INITIALIZER, useFactory: appInitializer, multi: true, deps: [AccountService] },
        { provide: HTTP_INTERCEPTORS, useClass: JwtInterceptor, multi: true },
        { provide: HTTP_INTERCEPTORS, useClass: ErrorInterceptor, multi: true },

        // provider used to create fake backend
        fakeBackendProvider
    ],
```

### Step 2: run the app

```bash
npm install
npm start
```

### How the fake backend behaves (important for beginners)

- Accounts are stored in your browser `localStorage`, not in a database.
- "Emails" (verification + reset password links) are displayed in the UI as alerts because a browser-only app can't send real emails.
- The first registered account becomes `Admin`, and all other accounts become `User`.

If you want a clean slate while using the fake backend, clear site date in your browser or remove the local storage key:

- `angular-15-setup-verification-boilerplate-accounts`

## 4) Using the app (what to click)

This section assumes you are starting fresh and want to see the full flow.

### A) Create an account

1. Go to Register
2. Fill in your details and submit
3. If you are using the fake backend, a "verification email" will appear as an alert with a link
4. Click the verification link (or paste it in the browser) to verify your account

### B) Login

1. Go to Login
2. Enter your email + password
3. On success you'll be redirected to the home page

### C) Forgot password + reset password

1. Go to Forgot Password
2. Enter your email and submit
3. If you are using the fake backend, a "reset password email" will appear as an alert with a link
4. Click the reset link and set a new password

### 5) How authentication works

This boilerplate uses two tokens:

 - Access token (JWT)