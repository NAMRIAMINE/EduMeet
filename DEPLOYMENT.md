# EduMeet Deployment Guide

This guide will help you deploy the EduMeet platform with:
- **Frontend (Frontea)** → Vercel
- **3 Backend Services** → Render
  - serverea (Main API - Port 5001)
  - Backea (Authentication - Port 5000)
  - back (AI Quiz Generator - Port 5003)

---

## Prerequisites

1. **GitHub Account** (for code repository)
2. **MongoDB Atlas Account** (free tier available at https://www.mongodb.com/cloud/atlas)
3. **Vercel Account** (free tier at https://vercel.com)
4. **Render Account** (free tier at https://render.com)
5. **Groq API Key** (for AI quiz generation at https://console.groq.com)
6. **Gmail Account** (for sending emails)

---

## Step 1: Set Up MongoDB Atlas

1. Go to https://www.mongodb.com/cloud/atlas
2. Create a free cluster
3. Create a database user with username and password
4. Whitelist all IPs: `0.0.0.0/0` (for cloud access)
5. Get your connection string:
   - Click "Connect" → "Connect your application"
   - Copy the connection string (looks like: `mongodb+srv://username:password@cluster.mongodb.net/`)
   - Replace `<password>` with your actual password
   - Add database name: `mongodb+srv://username:password@cluster.mongodb.net/edumeet?retryWrites=true&w=majority`

---

## Step 2: Deploy Backend Services to Render

### Option A: Using render.yaml (Recommended)

1. Push your code to GitHub
2. Go to https://dashboard.render.com
3. Click "New" → "Blueprint"
4. Connect your GitHub repository
5. Render will detect the `render.yaml` file
6. Set the environment variables for each service in the Render dashboard

### Option B: Manual Deployment (Alternative)

#### Deploy serverea (Main Backend)

1. Go to https://dashboard.render.com
2. Click "New" → "Web Service"
3. Connect your GitHub repository
4. Configure:
   - **Name**: `edumeet-serverea`
   - **Root Directory**: `serverea`
   - **Build Command**: `npm install`
   - **Start Command**: `npm start`
   - **Environment**: Node
5. Add environment variables:
   ```
   MONGO_URIE=mongodb+srv://username:password@cluster.mongodb.net/edumeet?retryWrites=true&w=majority
   JWT_SECRETA=your-super-secret-jwt-key-min-32-chars
   DEV_NO_AUTH=false
   YOUTUBE_API_KEY=your-youtube-api-key
   GOOGLE_API_KEY=your-google-api-key
   GOOGLE_CSE_ID=your-google-custom-search-engine-id
   NODE_ENV=production
   ```

   **Getting Google API Keys**:
   - YouTube API: https://console.cloud.google.com/apis/library/youtube.googleapis.com
   - Google Custom Search: https://console.cloud.google.com/apis/library/customsearch.googleapis.com
   - Create a Custom Search Engine: https://programmablesearchengine.google.com/

6. Click "Create Web Service"
7. **Copy the deployment URL** (e.g., `https://edumeet-serverea.onrender.com`)

#### Deploy Backea (Auth Backend)

1. Click "New" → "Web Service"
2. Connect your GitHub repository
3. Configure:
   - **Name**: `edumeet-backea`
   - **Root Directory**: `Backea`
   - **Build Command**: `npm install`
   - **Start Command**: `npm start`
   - **Environment**: Node
4. Add environment variables:
   ```
   MONGO_URI=mongodb+srv://username:password@cluster.mongodb.net/edumeet?retryWrites=true&w=majority
   JWT_SECRET=your-super-secret-jwt-key-min-32-chars
   EMAIL_USER=your-email@gmail.com
   EMAIL_PASS=your-gmail-app-password
   NODE_ENV=production
   ```

   **For EMAIL_PASS**:
   - Go to Google Account → Security → 2-Step Verification → App passwords
   - Generate an app password for "Mail"
   - Use that 16-character password

5. Click "Create Web Service"
6. **Copy the deployment URL** (e.g., `https://edumeet-backea.onrender.com`)

#### Deploy back (Quiz Backend)

1. Click "New" → "Web Service"
2. Connect your GitHub repository
3. Configure:
   - **Name**: `edumeet-quiz`
   - **Root Directory**: `back`
   - **Build Command**: `npm install`
   - **Start Command**: `npm start`
   - **Environment**: Node
4. Add environment variables:
   ```
   GROQ_API_KEY=your-groq-api-key
   NODE_ENV=production
   ```

   **Get Groq API Key**:
   - Go to https://console.groq.com
   - Sign up and create an API key

5. Click "Create Web Service"
6. **Copy the deployment URL** (e.g., `https://edumeet-quiz.onrender.com`)

---

## Step 3: Deploy Frontend to Vercel

1. Go to https://vercel.com
2. Click "Add New" → "Project"
3. Import your GitHub repository
4. Configure:
   - **Framework Preset**: Create React App
   - **Root Directory**: `Frontea`
   - **Build Command**: `npm run build`
   - **Output Directory**: `build`
5. Add environment variables (from the backend URLs you copied):
   ```
   REACT_APP_API_SERVEREA_URL=https://edumeet-serverea.onrender.com
   REACT_APP_API_BACKEA_URL=https://edumeet-backea.onrender.com
   REACT_APP_API_QUIZ_URL=https://edumeet-quiz.onrender.com
   ```
6. Click "Deploy"
7. Your frontend will be live at `https://your-project.vercel.app`

---

## Step 4: Test Your Deployment

1. Visit your Vercel frontend URL
2. Test the following features:
   - ✅ User registration
   - ✅ User login
   - ✅ Password reset
   - ✅ Search functionality
   - ✅ Quiz generation

---

## Important Notes

### Render Free Tier Limitations
- Services spin down after 15 minutes of inactivity
- First request after inactivity may take 30-60 seconds (cold start)
- Consider upgrading to paid tier for production use

### Environment Variables Security
- Never commit `.env` files to GitHub
- Use the `.env.example` files as templates
- Set environment variables directly in Vercel/Render dashboards

### CORS Configuration
All backends are already configured with CORS enabled via `cors()` middleware.

### MongoDB Connection
- Make sure to whitelist `0.0.0.0/0` in MongoDB Atlas Network Access
- Use the connection string with `retryWrites=true&w=majority`

---

## Troubleshooting

### Backend not responding
- Check Render logs: Dashboard → Your Service → Logs
- Verify environment variables are set correctly
- Ensure MongoDB Atlas IP whitelist includes `0.0.0.0/0`

### Frontend can't connect to backend
- Verify the backend URLs in Vercel environment variables
- Check browser console for CORS errors
- Ensure backend services are running (not spun down)

### Email not sending
- Verify Gmail credentials are correct
- Make sure you're using an App Password, not your regular Gmail password
- Check that 2-Step Verification is enabled on your Google account

### Quiz not generating
- Verify Groq API key is valid
- Check Render logs for the quiz backend
- Ensure you haven't exceeded Groq API rate limits

---

## Cost Breakdown

**Free Tier Setup (Suitable for development/testing):**
- MongoDB Atlas: Free (512MB storage)
- Render: Free (3 services with limitations)
- Vercel: Free (unlimited personal projects)
- Groq API: Free tier available

**Estimated Monthly Cost for Production:**
- MongoDB Atlas: $0-9 (depending on usage)
- Render: $21 (3 services × $7 each)
- Vercel: Free (or $20/month for Pro)
- Groq API: Pay as you go

---

## Next Steps

1. Set up custom domain in Vercel
2. Configure SSL certificates (automatic on Vercel/Render)
3. Set up monitoring and logging
4. Configure CI/CD pipeline for automatic deployments
5. Add error tracking (e.g., Sentry)

---

## Support

For issues or questions:
- Check Render logs for backend issues
- Check Vercel logs for frontend issues
- Verify all environment variables are set correctly
- Ensure MongoDB Atlas is accessible

---

## Files Reference

- `Frontea/.env.example` - Frontend environment variables template
- `serverea/.env.example` - Main backend environment variables template
- `Backea/.env.example` - Auth backend environment variables template
- `back/.env.example` - Quiz backend environment variables template
- `render.yaml` - Render blueprint configuration (optional)
- `Frontea/vercel.json` - Vercel configuration

---

**Last Updated**: January 2026
