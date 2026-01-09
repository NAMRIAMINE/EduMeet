# 🆓 FREE Deployment Guide - EduMeet Platform

Deploy your entire EduMeet platform (Frontend + 3 Backends) **completely FREE** using Vercel!

---

## 🎯 Why Vercel Free Tier?

- ✅ **100% FREE** for personal projects (no credit card required)
- ✅ Deploy unlimited projects
- ✅ Automatic HTTPS/SSL certificates
- ✅ Global CDN for fast performance
- ✅ Automatic deployments from GitHub
- ✅ Environment variables support
- ✅ 100GB bandwidth per month (generous free tier)

---

## 📋 Prerequisites

1. **GitHub Account** ✅ (You already have this!)
2. **Vercel Account** - Sign up at https://vercel.com (use your GitHub account)
3. **MongoDB Atlas** - Free tier at https://www.mongodb.com/cloud/atlas
4. **Groq API Key** - Free at https://console.groq.com
5. **Gmail Account** - For sending emails

---

## Step 1: Set Up MongoDB Atlas (5 minutes)

1. Go to https://www.mongodb.com/cloud/atlas
2. Click "Try Free" and sign up
3. Create a **FREE** M0 cluster (512MB storage)
4. Click "Database Access" → Create user with username/password
5. Click "Network Access" → "Add IP Address" → "Allow Access from Anywhere" (0.0.0.0/0)
6. Click "Connect" → "Connect your application"
7. Copy the connection string:
   ```
   mongodb+srv://username:password@cluster.mongodb.net/?retryWrites=true&w=majority
   ```

---

## Step 2: Get API Keys (5 minutes)

### Groq API Key (for Quiz Generator)
1. Go to https://console.groq.com
2. Sign up (FREE)
3. Create an API key
4. Copy and save it

### Google API Keys (for Search Features)
1. Go to https://console.cloud.google.com
2. Create a new project
3. Enable these APIs:
   - YouTube Data API v3
   - Custom Search API
4. Create API credentials (API Key)
5. Create a Custom Search Engine at https://programmablesearchengine.google.com/

### Gmail App Password (for Email)
1. Go to your Google Account → Security
2. Enable 2-Step Verification
3. Go to "App passwords"
4. Generate a password for "Mail"
5. Copy the 16-character password

---

## Step 3: Deploy Backends to Vercel (15 minutes)

You'll deploy **4 projects** on Vercel (all FREE):
1. Frontend (Frontea)
2. Backend 1 (serverea)
3. Backend 2 (Backea)
4. Backend 3 (back)

### 3.1 Deploy serverea (Main Backend)

1. Go to https://vercel.com/dashboard
2. Click "Add New" → "Project"
3. Select your GitHub repository: **NAMRIAMINE/EduMeet**
4. Configure:
   - **Project Name**: `edumeet-serverea`
   - **Framework Preset**: Other
   - **Root Directory**: `serverea`
   - **Build Command**: (leave empty)
   - **Output Directory**: (leave empty)
5. Click "Environment Variables" and add:
   ```
   MONGO_URIE=mongodb+srv://username:password@cluster.mongodb.net/?retryWrites=true&w=majority
   JWT_SECRETA=your-super-secret-jwt-key-here
   DEV_NO_AUTH=false
   YOUTUBE_API_KEY=your-youtube-api-key
   GOOGLE_API_KEY=your-google-api-key
   GOOGLE_CSE_ID=your-google-cse-id
   ```
6. Click "Deploy"
7. **Copy the deployment URL**: `https://edumeet-serverea.vercel.app`

### 3.2 Deploy Backea (Auth Backend)

1. Click "Add New" → "Project"
2. Select your GitHub repository again
3. Configure:
   - **Project Name**: `edumeet-backea`
   - **Framework Preset**: Other
   - **Root Directory**: `Backea`
4. Add environment variables:
   ```
   MONGO_URI=mongodb+srv://username:password@cluster.mongodb.net/?retryWrites=true&w=majority
   JWT_SECRET=your-super-secret-jwt-key-here
   EMAIL_USER=your-email@gmail.com
   EMAIL_PASS=your-16-char-app-password
   ```
5. Click "Deploy"
6. **Copy the deployment URL**: `https://edumeet-backea.vercel.app`

### 3.3 Deploy back (Quiz Backend)

1. Click "Add New" → "Project"
2. Select your GitHub repository again
3. Configure:
   - **Project Name**: `edumeet-quiz`
   - **Framework Preset**: Other
   - **Root Directory**: `back`
4. Add environment variables:
   ```
   GROQ_API_KEY=your-groq-api-key-here
   ```
5. Click "Deploy"
6. **Copy the deployment URL**: `https://edumeet-quiz.vercel.app`

---

## Step 4: Deploy Frontend to Vercel (5 minutes)

1. Click "Add New" → "Project"
2. Select your GitHub repository again
3. Configure:
   - **Project Name**: `edumeet-frontend`
   - **Framework Preset**: Create React App
   - **Root Directory**: `Frontea`
   - **Build Command**: `npm run build`
   - **Output Directory**: `build`
4. Add environment variables (use the URLs from steps above):
   ```
   REACT_APP_API_SERVEREA_URL=https://edumeet-serverea.vercel.app
   REACT_APP_API_BACKEA_URL=https://edumeet-backea.vercel.app
   REACT_APP_API_QUIZ_URL=https://edumeet-quiz.vercel.app
   ```
5. Click "Deploy"
6. Your app will be live at: `https://edumeet-frontend.vercel.app` 🎉

---

## Step 5: Test Your Deployment (5 minutes)

1. Visit your frontend URL: `https://edumeet-frontend.vercel.app`
2. Test features:
   - ✅ User Registration
   - ✅ User Login
   - ✅ Password Reset (check email)
   - ✅ Search functionality
   - ✅ Quiz generation

---

## 🔧 Troubleshooting

### Backend returns 404 or 500 errors
- Check Vercel logs: Project → Deployments → Click deployment → "View Function Logs"
- Verify all environment variables are set correctly
- Make sure MongoDB Atlas allows connections from 0.0.0.0/0

### Frontend can't connect to backends
- Open browser console (F12) to see errors
- Verify backend URLs in frontend environment variables
- Make sure backend URLs don't have trailing slashes

### Email not sending
- Verify you're using Gmail App Password (not regular password)
- Check that 2-Step Verification is enabled
- Test email credentials

### Quiz not generating
- Verify Groq API key is valid
- Check Groq API usage limits (free tier has limits)
- Check function logs on Vercel

---

## 💰 Cost Breakdown

**Total Monthly Cost: $0.00 (FREE)**

| Service | Plan | Cost |
|---------|------|------|
| Vercel (4 projects) | Free Tier | $0 |
| MongoDB Atlas | M0 Free Tier | $0 |
| Groq API | Free Tier | $0 |
| Google APIs | Free Tier | $0 |
| **TOTAL** | | **$0** |

### Free Tier Limits:
- **Vercel**: 100GB bandwidth/month, unlimited projects
- **MongoDB Atlas**: 512MB storage, unlimited connections
- **Groq**: Generous free tier for API calls
- **Google APIs**: 10,000 requests/day (YouTube), 100 queries/day (Custom Search)

---

## 🚀 Automatic Deployments

Every time you push to GitHub, Vercel will automatically:
1. Detect the changes
2. Build your projects
3. Deploy the updates
4. Show you a preview URL

No manual deployment needed! 🎉

---

## 🔒 Security Notes

- ✅ All connections use HTTPS automatically
- ✅ Environment variables are encrypted
- ✅ Never commit `.env` files to GitHub
- ✅ MongoDB connection uses secure SSL
- ✅ Gmail uses app-specific passwords

---

## 📱 Custom Domain (Optional)

Want your own domain? You can add it for FREE:

1. Buy a domain (e.g., from Namecheap, ~$10/year)
2. Go to Vercel Project → Settings → Domains
3. Add your domain
4. Update DNS records as instructed
5. Vercel automatically provides FREE SSL certificate

---

## 🎯 Next Steps

1. ✅ Test all features thoroughly
2. ✅ Add more content/features
3. ✅ Monitor usage in Vercel dashboard
4. ✅ Share your app with users!

---

## 🆘 Need Help?

- **Vercel Docs**: https://vercel.com/docs
- **MongoDB Atlas Docs**: https://docs.atlas.mongodb.com
- **Groq API Docs**: https://console.groq.com/docs

---

## 🎉 Congratulations!

Your EduMeet platform is now:
- ✅ Deployed and live
- ✅ 100% FREE
- ✅ Globally accessible
- ✅ Automatically updated
- ✅ Production-ready

**Share your app with the world!** 🌍

---

**Last Updated**: January 2026
**Deployment Platform**: Vercel (Free Tier)
