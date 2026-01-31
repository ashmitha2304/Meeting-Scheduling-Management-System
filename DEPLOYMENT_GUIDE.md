# 🚀 GITHUB PUSH & RENDER DEPLOYMENT GUIDE

## ✅ REPOSITORIES READY

All three repositories are initialized and ready to push:

### 1️⃣ **Backend Repository**

- **URL**: https://github.com/ashmitha2304/Meeting-Scheduling-Management-System-Backend
- **Files**: 29 files (Node.js + Express + MongoDB + TypeScript)
- **Status**: ✅ Ready to push

### 2️⃣ **Frontend Repository**

- **URL**: https://github.com/ashmitha2304/Meeting-Scheduling-Management-System-Frontend
- **Files**: 22 files (React + TypeScript + Vite)
- **Status**: ✅ Ready to push

### 3️⃣ **Combined Repository**

- **URL**: https://github.com/ashmitha2304/Meeting-Scheduling-Management-System
- **Files**: Complete project (Backend + Frontend)
- **Status**: ✅ Ready to push

---

## 🔐 STEP 1: CREATE GITHUB PERSONAL ACCESS TOKEN

Before pushing, you need a GitHub Personal Access Token:

1. Go to: https://github.com/settings/tokens
2. Click **"Generate new token (classic)"**
3. Name: `Meeting-Scheduler-Deploy`
4. Select scope: **✅ repo** (full control of private repositories)
5. Click **"Generate token"**
6. **COPY THE TOKEN** (you'll only see it once!)
7. Save it somewhere safe - you'll use it as your password

---

## 📤 STEP 2: PUSH TO GITHUB

Run these commands **one at a time** in PowerShell:

### Push Backend:

```powershell
cd d:\SchedulingSystem\backend
git push -u origin main
```

**When prompted:**

- Username: `ashmitha2304`
- Password: _[Paste your GitHub Personal Access Token]_

---

### Push Frontend:

```powershell
cd d:\SchedulingSystem\frontend
git push -u origin main
```

**When prompted:**

- Username: `ashmitha2304`
- Password: _[Paste your GitHub Personal Access Token]_

---

### Push Complete Project:

```powershell
cd d:\SchedulingSystem
git push -u origin main
```

**When prompted:**

- Username: `ashmitha2304`
- Password: _[Paste your GitHub Personal Access Token]_

---

## 🌐 STEP 3: DEPLOY BACKEND TO RENDER

### **Render Repository Link:**

```
https://github.com/ashmitha2304/Meeting-Scheduling-Management-System-Backend
```

### **Deployment Steps:**

1. **Go to Render**: https://render.com
2. **Sign Up/Login** with GitHub
3. Click **"New +"** → **"Web Service"**
4. **Connect GitHub Repository**:
   - Select: `Meeting-Scheduling-Management-System-Backend`
   - Click **"Connect"**

5. **Configure Service**:

   ```
   Name: meeting-scheduler-backend
   Region: Oregon (US West) or closest to you
   Branch: main
   Root Directory: (leave blank)
   Runtime: Node
   Build Command: npm install && npm run build
   Start Command: npm start
   Instance Type: Free
   ```

6. **Add Environment Variables** (Click "Advanced" → "Add Environment Variable"):

   ```env
   NODE_ENV=production
   PORT=5000
   MONGODB_URI=mongodb+srv://meetingUser:meetingUser@m0.smalwny.mongodb.net/meeting-scheduler?retryWrites=true&w=majority&appName=M0
   JWT_SECRET=yi4m9OMQ8fh5gRIEN5Xshy4Yqa7lg1T7NTioitCmL8E0ieniHmJn7rUfYKIWMSmfdBq6q0ZWauoIcLbT42LA+w==
   JWT_REFRESH_SECRET=H1gi7KzPdg9v9SiZ7ScdZA1F9t+Trkl8TScSsrG7Wxm4tVloF5PHuoqns9grqHUYLAkygYEt9rwdGonTK8rbkQ==
   JWT_EXPIRES_IN=1h
   JWT_REFRESH_EXPIRES_IN=7d
   BCRYPT_SALT_ROUNDS=12
   CLIENT_URL=https://your-frontend-url.vercel.app
   ALLOWED_ORIGINS=https://your-frontend-url.vercel.app
   ```

   **Note**: You'll update `CLIENT_URL` and `ALLOWED_ORIGINS` after deploying frontend

7. Click **"Create Web Service"**

8. **Wait 3-5 minutes** for deployment

9. **Your Backend URL** will be:

   ```
   https://meeting-scheduler-backend-[unique-id].onrender.com
   ```

10. **Verify Deployment**:
    ```
    https://meeting-scheduler-backend-[your-id].onrender.com/health
    ```
    Should return: `{"status":"ok","mongodb":"connected",...}`

---

## 🎨 STEP 4: DEPLOY FRONTEND TO VERCEL

### **Frontend Repository Link:**

```
https://github.com/ashmitha2304/Meeting-Scheduling-Management-System-Frontend
```

### **Deployment Steps:**

1. **Go to Vercel**: https://vercel.com
2. **Sign Up/Login** with GitHub
3. Click **"Add New Project"**
4. **Import Repository**:
   - Select: `Meeting-Scheduling-Management-System-Frontend`
   - Click **"Import"**

5. **Configure Project**:

   ```
   Framework Preset: Vite
   Root Directory: ./
   Build Command: npm run build
   Output Directory: dist
   Install Command: npm install
   ```

6. **Environment Variables**:
   - Click **"Environment Variables"**
   - Add:
     ```
     Name: VITE_API_BASE_URL
     Value: https://meeting-scheduler-backend-[your-id].onrender.com
     ```
   - Use your actual Render backend URL

7. Click **"Deploy"**

8. **Wait 2-3 minutes** for deployment

9. **Your Frontend URL** will be:
   ```
   https://meeting-scheduler-[unique-id].vercel.app
   ```

---

## 🔄 STEP 5: UPDATE CORS SETTINGS

After frontend deployment, update backend CORS:

1. Go back to **Render Dashboard**
2. Select your **meeting-scheduler-backend** service
3. Go to **"Environment"** tab
4. Update these variables with your Vercel URL:
   ```
   CLIENT_URL=https://meeting-scheduler-[your-id].vercel.app
   ALLOWED_ORIGINS=https://meeting-scheduler-[your-id].vercel.app
   ```
5. Click **"Save Changes"**
6. Render will **automatically redeploy** (takes 1-2 minutes)

---

## ✅ VERIFICATION CHECKLIST

After all deployments:

- [ ] Backend pushed to GitHub
- [ ] Frontend pushed to GitHub
- [ ] Combined project pushed to GitHub
- [ ] Backend deployed to Render
- [ ] Backend health check works: `/health` returns 200
- [ ] Backend MongoDB shows "connected"
- [ ] Frontend deployed to Vercel
- [ ] Frontend loads without errors
- [ ] CORS updated with Vercel URL
- [ ] Can register new user
- [ ] Can login
- [ ] Dashboard loads correctly

---

## 🔗 REPOSITORY LINKS FOR RENDER

**When Render asks for repository, use:**

```
https://github.com/ashmitha2304/Meeting-Scheduling-Management-System-Backend
```

**Branch to deploy:**

```
main
```

---

## 📋 FINAL URLS TO SUBMIT

After deployment, you'll have:

1. **Backend GitHub**: https://github.com/ashmitha2304/Meeting-Scheduling-Management-System-Backend
2. **Frontend GitHub**: https://github.com/ashmitha2304/Meeting-Scheduling-Management-System-Frontend
3. **Combined GitHub**: https://github.com/ashmitha2304/Meeting-Scheduling-Management-System
4. **Backend Render**: https://meeting-scheduler-backend-[your-id].onrender.com
5. **Frontend Vercel**: https://meeting-scheduler-[your-id].vercel.app

---

## 🆘 TROUBLESHOOTING

### Issue: Git push fails with 403 error

**Solution**: You're using a different GitHub account. Use Personal Access Token instead of password.

### Issue: Render build fails

**Solution**:

- Check build logs in Render dashboard
- Verify all environment variables are set
- Ensure Node version is 18+

### Issue: MongoDB connection fails on Render

**Solution**:

- Verify `MONGODB_URI` is correct in Render environment variables
- Check MongoDB Atlas Network Access allows `0.0.0.0/0`
- Check MongoDB Atlas cluster is Active

### Issue: Frontend can't connect to backend

**Solution**:

- Verify `VITE_API_BASE_URL` in Vercel matches Render URL
- Check CORS settings in Render (CLIENT_URL and ALLOWED_ORIGINS)
- Redeploy backend after CORS update

---

## 🎯 QUICK REFERENCE

**Git Config:**

```
User: ashmitha2304
Email: ashmitha2304@gmail.com
```

**Render Repository:**

```
https://github.com/ashmitha2304/Meeting-Scheduling-Management-System-Backend
```

**Build Command (Render):**

```
npm install && npm run build
```

**Start Command (Render):**

```
npm start
```

---

**Ready to deploy! Start with STEP 1 above.** 🚀
