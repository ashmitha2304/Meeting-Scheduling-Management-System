# 🚨 GITHUB AUTHENTICATION REQUIRED

## ⚠️ Current Issue

You're currently authenticated as **SanjaiSrivatsan** but need to push as **ashmitha2304**.

## 🔐 SOLUTION: Create GitHub Personal Access Token

### Step 1: Create Token

1. Go to: https://github.com/settings/tokens
2. Click **"Generate new token (classic)"**
3. Settings:
   - **Name**: `Meeting-Scheduler-Deploy`
   - **Expiration**: 90 days
   - **Scopes**: ✅ **repo** (Full control of private repositories)
4. Click **"Generate token"**
5. **COPY THE TOKEN** (you'll only see it once!)
6. Save it in a secure location

### Step 2: Clear Old Credentials

```powershell
# Remove old GitHub credentials
cmdkey /list | Select-String "git:https://github.com" | ForEach-Object { cmdkey /delete:($_ -replace '.*Target: ','') }
```

### Step 3: Push Repositories

Run these commands **one at a time**:

#### Push Backend:

```powershell
cd d:\SchedulingSystem\backend
git push -u origin main
```

**When prompted:**

- Username: `ashmitha2304`
- Password: _[Paste your Personal Access Token]_

---

#### Push Frontend:

```powershell
cd d:\SchedulingSystem\frontend
git push -u origin main
```

**When prompted:**

- Username: `ashmitha2304`
- Password: _[Paste your Personal Access Token]_

---

#### Push Complete Project:

```powershell
cd d:\SchedulingSystem
git push -u origin main
```

**When prompted:**

- Username: `ashmitha2304`
- Password: _[Paste your Personal Access Token]_

---

## 📝 ALTERNATIVE: Use GitHub CLI

If you prefer, you can use GitHub CLI:

```powershell
# Install GitHub CLI (if not installed)
winget install --id GitHub.cli

# Authenticate
gh auth login

# Then push normally
cd d:\SchedulingSystem\backend
git push -u origin main

cd d:\SchedulingSystem\frontend
git push -u origin main

cd d:\SchedulingSystem
git push -u origin main
```

---

## ✅ VERIFICATION

After successful push, verify on GitHub:

1. **Backend**: https://github.com/ashmitha2304/Meeting-Scheduling-Management-System-Backend
2. **Frontend**: https://github.com/ashmitha2304/Meeting-Scheduling-Management-System-Frontend
3. **Complete**: https://github.com/ashmitha2304/Meeting-Scheduling-Management-System

Each repository should show:

- ✅ Recent commit
- ✅ All files visible
- ✅ README displayed

---

## 🌐 NEXT: RENDER DEPLOYMENT

After pushing to GitHub, deploy to Render:

**Repository for Render:**

```
https://github.com/ashmitha2304/Meeting-Scheduling-Management-System-Backend
```

See [DEPLOYMENT_GUIDE.md](DEPLOYMENT_GUIDE.md) for full Render setup instructions.

---

## 🆘 TROUBLESHOOTING

### Issue: "Permission denied to SanjaiSrivatsan"

**Solution**: You need to authenticate as ashmitha2304. Use Personal Access Token as password.

### Issue: Windows doesn't prompt for credentials

**Solution**:

```powershell
git config --global --unset credential.helper
git config --global credential.helper manager
```

Then try pushing again.

### Issue: Token doesn't work

**Solution**:

- Verify token has 'repo' scope
- Token should be pasted as password (not username)
- Username should be 'ashmitha2304'

---

**Start with Step 1 above to create your Personal Access Token!** 🔑
