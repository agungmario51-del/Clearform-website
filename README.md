# ClearForm — name registration website

A small, mobile-friendly website with a public name form and a password-protected owner dashboard.

## Included
- Public registration form: `/`
- Saves full names in a local SQLite database
- Owner dashboard: `/admin`
- Login page: `/admin/login`
- Password hashing, login rate limiting, secure session cookies in production, and basic security headers

## Before publishing
You need a Node.js 20+ host that supports a persistent disk/volume. SQLite data must live on persistent storage or registrations may be lost when the host restarts/redeploys. For a production service, configure the host's persistent disk and set `data/` as its mount path.

### 1. Create your admin password hash
On your computer, in this project folder, run:

```bash
node -e "const b=require('bcryptjs'); console.log(b.hashSync('CHOOSE-A-LONG-UNIQUE-PASSWORD', 12))"
```

Replace the sample password in that command with your own strong password. Copy the resulting hash.

### 2. Configure environment variables
Copy `.env.example` to `.env`, then set:
- `SESSION_SECRET`: a long random secret (at least 32 random characters)
- `ADMIN_USERNAME`: your chosen admin username
- `ADMIN_PASSWORD_HASH`: the bcrypt hash from step 1
- `NODE_ENV=production` on your live host

Do not share your `.env` file or commit it to a public repository.

### 3. Run locally
```bash
npm install
npm start
```
Open `http://localhost:3000`. Admin access is at `http://localhost:3000/admin/login`.

## Deploying
Deploy this folder to a Node.js hosting provider such as Render or Railway. Set the start command to `npm start`, add the environment variables above, enable HTTPS, and attach persistent storage mounted at the project's `data` directory. Check your provider's current instructions and pricing before choosing a plan.

## Privacy note
This starter collects only a full name. Before making it public, add a clear explanation of why names are collected, how long they are retained, and how a person can request deletion. Do not collect sensitive information you do not need. Protect the admin login and periodically back up the database.
