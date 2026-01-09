# Update Vercel Frontend Environment Variables

Your frontend is currently trying to connect to `localhost` which doesn't work in production. You need to update the environment variables in Vercel to point to your deployed backends.

## 🔗 Your Deployed URLs:

- **Frontend**: https://edu-meet-six.vercel.app
- **serverea**: https://edu-meet-serverea-namri.vercel.app
- **Backea**: https://edu-meet-backea-psi.vercel.app
- **back (Quiz)**: https://edu-meet-back.vercel.app

---

## 📝 Step-by-Step: Update Environment Variables in Vercel

### Step 1: Go to Your Frontend Project
1. Visit https://vercel.com/dashboard
2. Click on your frontend project: **edu-meet-six**

### Step 2: Open Settings
1. Click on **"Settings"** tab at the top
2. Click on **"Environment Variables"** in the left sidebar

### Step 3: Update/Add Environment Variables

You need to add these **3 environment variables**:

#### Variable 1: REACT_APP_API_SERVEREA_URL
- **Key**: `REACT_APP_API_SERVEREA_URL`
- **Value**: `https://edu-meet-serverea-namri.vercel.app`
- **Environments**: Check all (Production, Preview, Development)
- Click **"Save"**

#### Variable 2: REACT_APP_API_BACKEA_URL
- **Key**: `REACT_APP_API_BACKEA_URL`
- **Value**: `https://edu-meet-backea-psi.vercel.app`
- **Environments**: Check all (Production, Preview, Development)
- Click **"Save"**

#### Variable 3: REACT_APP_API_QUIZ_URL
- **Key**: `REACT_APP_API_QUIZ_URL`
- **Value**: `https://edu-meet-back.vercel.app`
- **Environments**: Check all (Production, Preview, Development)
- Click **"Save"**

### Step 4: Delete Old Variables (if they exist)
If you see these old localhost URLs, delete them:
- Any variable with `localhost:5000`
- Any variable with `localhost:5001`
- Any variable with `localhost:5003`

---

## 🚀 Step 5: Redeploy Your Frontend

After adding the environment variables, you **MUST** redeploy for them to take effect:

### Option A: Automatic Redeploy (Easiest)
1. Go to the **"Deployments"** tab
2. Click on the latest deployment
3. Click the **"..."** menu (three dots) in the top right
4. Click **"Redeploy"**
5. **IMPORTANT**: Make sure "Use existing Build Cache" is **UNCHECKED** ❌
6. Click **"Redeploy"** button
7. Wait 2-3 minutes for the build to complete

### Option B: Manual Git Push (Alternative)
You can also just make a small change and push to GitHub, which will trigger auto-deploy.

---

## ✅ Step 6: Test Your Deployed Application

After redeployment completes:

1. Visit: https://edu-meet-six.vercel.app
2. Try to **register** a new account
3. Try to **login**
4. Try to **search** for something
5. Try to **generate a quiz**

Everything should work now! 🎉

---

## 🧪 Quick Test: Check Backend Connectivity

You can test if the backends are accessible:

### Test serverea:
Open in browser: https://edu-meet-serverea-namri.vercel.app/
**Expected**: JSON response with API documentation

### Test Backea:
Open in browser: https://edu-meet-backea-psi.vercel.app/
**Expected**: JSON response with auth backend status

### Test back (Quiz):
Open in browser: https://edu-meet-back.vercel.app/
**Expected**: JSON response with quiz backend status

---

## ⚠️ Common Issues:

### Issue 1: Still seeing "Erreur serveur"
- **Solution**: Make sure you redeployed WITHOUT build cache
- Go to Deployments → Redeploy → Uncheck "Use existing Build Cache"

### Issue 2: CORS errors in browser console
- **Solution**: All backends have CORS enabled, but double-check backend logs in Vercel

### Issue 3: "Cannot read environment variables"
- **Solution**: Make sure the variable names are EXACTLY as shown (case-sensitive)
- They must start with `REACT_APP_`

---

## 📋 Environment Variables Summary

### Frontend (Frontea) - Copy-paste these into Vercel Dashboard:

```
REACT_APP_API_SERVEREA_URL=https://edu-meet-serverea-namri.vercel.app
REACT_APP_API_BACKEA_URL=https://edu-meet-backea-psi.vercel.app
REACT_APP_API_QUIZ_URL=https://edu-meet-back.vercel.app
```

### Backea (Auth Backend) - Also add this environment variable:

Go to your **Backea** project in Vercel Dashboard → Settings → Environment Variables

Add this variable:
- **Key**: `FRONTEND_URL`
- **Value**: `https://edu-meet-six.vercel.app`
- **Environments**: Check all (Production, Preview, Development)
- Click **"Save"**

**Important**: After adding this, redeploy the Backea backend so email verification and password reset links work correctly!

---

## 🎯 After This Update:

Your frontend will:
- ✅ Connect to the deployed backends (not localhost)
- ✅ Allow users to register and login
- ✅ Enable search functionality
- ✅ Generate AI quizzes
- ✅ Send password reset emails

---

**Good luck! Your app should be fully functional after this update!** 🚀
