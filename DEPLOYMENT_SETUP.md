# Deployment Setup Guide

## 1. MongoDB Atlas (Cloud Database)

### Step 1: Create MongoDB Atlas Account

1. Go to https://www.mongodb.com/cloud/atlas/register
2. Sign up for a free account
3. Click "Build a Database" → Choose "M0 FREE" tier

### Step 2: Create Database User

1. In Atlas dashboard, go to "Database Access" (left sidebar)
2. Click "Add New Database User"
3. Choose "Password" authentication
4. Set username: `meetingUser`
5. Set password: `meetingUser`
6. Under "Database User Privileges", select "Read and write to any database"
7. Click "Add User"

### Step 3: Allow IP Access (0.0.0.0/0)

1. Go to "Network Access" (left sidebar)
2. Click "Add IP Address"
3. Click "Allow Access from Anywhere"
4. This will add `0.0.0.0/0` (allows all IPs)
5. Click "Confirm"

### Step 4: Get Connection String

1. Go to "Database" (left sidebar)
2. Click "Connect" on your cluster
3. Choose "Connect your application"
4. Select "Node.js" driver and version "5.5 or later"
5. Copy the connection string, it looks like:
   ```
   mongodb+srv://<username>:<password>@cluster0.xxxxx.mongodb.net/?retryWrites=true&w=majority
   ```
6. Replace `<username>` with your username
7. Replace `<password>` with your actual password
8. Add database name after `.net/`: `meeting-scheduler`

**Final URL Example:**

```
mongodb+srv://meetingUser:meetingUser@m0.smalwny.mongodb.net/meeting-scheduler?appName=M0
```

---

## 2. GitHub Repositories

### Create Backend Repository

```bash
# Navigate to backend folder
cd d:\SchedulingSystem\backend

# Initialize git (if not already done)
git init

# Create .gitignore
echo "node_modules/
.env
dist/
*.log
.DS_Store" > .gitignore

# Add all files
git add .

# Commit
git commit -m "Initial commit: Meeting Scheduler Backend"

# Create repository on GitHub (https://github.com/new)
# Then connect and push:
git remote add origin https://github.com/YOUR_USERNAME/meeting-scheduler-backend.git
git branch -M main
git push -u origin main
```

### Create Frontend Repository

```bash
# Navigate to frontend folder
cd d:\SchedulingSystem\frontend

# Initialize git
git init

# Create .gitignore
echo "node_modules/
dist/
.env
*.log
.DS_Store" > .gitignore

# Add all files
git add .

# Commit
git commit -m "Initial commit: Meeting Scheduler Frontend"

# Create repository on GitHub
git remote add origin https://github.com/YOUR_USERNAME/meeting-scheduler-frontend.git
git branch -M main
git push -u origin main
```

---

## 3. Deploy Backend to Render

### Step 1: Sign up for Render

1. Go to https://render.com
2. Sign up (use GitHub to sign in)

### Step 2: Create Web Service

1. Click "New +" → "Web Service"
2. Connect your GitHub account
3. Select `meeting-scheduler-backend` repository
4. Configure:
   - **Name**: `meeting-scheduler-api`
   - **Region**: Choose closest to you
   - **Branch**: `main`
   - **Root Directory**: Leave blank (or `backend` if monorepo)
   - **Runtime**: `Node`
   - **Build Command**: `npm install && npm run build`
   - **Start Command**: `npm start`
   - **Plan**: Free

### Step 3: Add Environment Variables

In Render dashboard, go to "Environment" tab and add:

```
NODE_ENV=production
PORT=5000
MONGODB_URI=<Your MongoDB Atlas connection string from Step 1>
JWT_SECRET=<Generate with: openssl rand -base64 64>
JWT_REFRESH_SECRET=<Generate another one>
JWT_EXPIRES_IN=1h
JWT_REFRESH_EXPIRES_IN=7d
BCRYPT_SALT_ROUNDS=12
CLIENT_URL=<Your frontend URL - add after deploying frontend>
ALLOWED_ORIGINS=<Your frontend URL>
```

### Step 4: Deploy

- Click "Create Web Service"
- Wait for deployment (5-10 minutes)
- Your backend URL will be: `https://meeting-scheduler-api.onrender.com`

---

## 4. Deploy Frontend to Vercel

### Step 1: Sign up for Vercel

1. Go to https://vercel.com
2. Sign up with GitHub

### Step 2: Import Project

1. Click "Add New" → "Project"
2. Import `meeting-scheduler-frontend` repository
3. Configure:
   - **Framework Preset**: Vite
   - **Root Directory**: Leave blank (or `frontend` if monorepo)
   - **Build Command**: `npm run build`
   - **Output Directory**: `dist`

### Step 3: Add Environment Variable

Add in Vercel dashboard:

```
VITE_API_BASE_URL=https://meeting-scheduler-api.onrender.com/api
```

### Step 4: Deploy

- Click "Deploy"
- Your frontend URL will be: `https://meeting-scheduler-frontend.vercel.app`

### Step 5: Update Backend Environment Variables

Go back to Render and update:

```
CLIENT_URL=https://meeting-scheduler-frontend.vercel.app
ALLOWED_ORIGINS=https://meeting-scheduler-frontend.vercel.app
```

---

## 5. Test Deployment

### Backend Health Check

```bash
curl https://meeting-scheduler-api.onrender.com/health
```

### Frontend

Open browser: `https://meeting-scheduler-frontend.vercel.app`

### Test Login

```bash
curl -X POST https://meeting-scheduler-api.onrender.com/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "organizer@example.com",
    "password": "Password123!"
  }'
```

---

## 6. Fill Out the Form

Once deployed, fill in the form with:

1. **MongoDB Cluster URL**: `mongodb+srv://meetingSchedulerUser:YourPassword@cluster0.xxxxx.mongodb.net/meeting-scheduler?retryWrites=true&w=majority`
2. **Backend GitHub Repository**: `https://github.com/YOUR_USERNAME/meeting-scheduler-backend`
3. **Frontend GitHub Repository**: `https://github.com/YOUR_USERNAME/meeting-scheduler-frontend`
4. **Backend Live Deployment Link**: `https://meeting-scheduler-api.onrender.com`

---

## Troubleshooting

### Render Deployment Issues

- Check build logs in Render dashboard
- Ensure `package.json` has correct `start` script
- Verify all environment variables are set

### MongoDB Connection Issues

- Verify IP whitelist includes `0.0.0.0/0`
- Check username/password in connection string
- Ensure database user has read/write permissions

### CORS Issues

- Verify `ALLOWED_ORIGINS` in backend matches frontend URL exactly
- Check frontend is using correct `VITE_API_BASE_URL`

### Frontend Not Loading

- Check browser console for errors
- Verify `VITE_API_BASE_URL` environment variable
- Ensure backend is running and accessible

---

## Quick Setup Commands

### Generate JWT Secrets (Git Bash or Linux)

```bash
# JWT Secret
openssl rand -base64 64

# JWT Refresh Secret
openssl rand -base64 64
```

### Generate JWT Secrets (PowerShell)

```powershell
# JWT Secret
[Convert]::ToBase64String([System.Text.Encoding]::UTF8.GetBytes((New-Guid).Guid + (New-Guid).Guid))

# JWT Refresh Secret
[Convert]::ToBase64String([System.Text.Encoding]::UTF8.GetBytes((New-Guid).Guid + (New-Guid).Guid))
```
