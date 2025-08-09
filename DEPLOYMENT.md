# Deployment Guide for Notes Mate

## Prerequisites

Before deploying, ensure you have:
- A Firebase project set up with Authentication enabled
- A backend API deployed (if using external backend)
- Environment variables configured

## 1. GitHub Setup

1. Create a new repository on GitHub
2. Initialize git in your project:
   ```bash
   git init
   git add .
   git commit -m "Initial commit - Notes Mate by Sujal Parmar"
   git branch -M main
   git remote add origin https://github.com/yourusername/notes-mate.git
   git push -u origin main
   ```

## 2. Vercel Deployment

### Option A: Deploy via Vercel CLI
1. Install Vercel CLI: `npm i -g vercel`
2. Run `vercel` in your project directory
3. Follow the prompts to deploy

### Option B: Deploy via Vercel Dashboard
1. Go to [vercel.com](https://vercel.com) and sign in
2. Click "New Project"
3. Import your GitHub repository
4. Configure the following settings:
   - **Framework Preset**: Vite
   - **Build Command**: `npm run build`
   - **Output Directory**: `dist`
   - **Install Command**: `npm install`

5. Add environment variables:
   ```
   VITE_API_BASE_URL=https://your-backend-url.com/api
   VITE_FIREBASE_API_KEY=your_firebase_api_key
   VITE_FIREBASE_AUTH_DOMAIN=your_project_id.firebaseapp.com
   VITE_FIREBASE_PROJECT_ID=your_project_id
   VITE_FIREBASE_STORAGE_BUCKET=your_project_id.appspot.com
   VITE_FIREBASE_MESSAGING_SENDER_ID=your_messaging_sender_id
   VITE_FIREBASE_APP_ID=your_app_id
   VITE_FIREBASE_MEASUREMENT_ID=your_measurement_id
   ```

6. Click "Deploy"

## 3. Render Deployment

1. Go to [render.com](https://render.com) and sign in
2. Click "New" → "Static Site"
3. Connect your GitHub repository
4. Configure the following:
   - **Name**: notes-mate
   - **Branch**: main
   - **Build Command**: `npm run build`
   - **Publish Directory**: `dist`

5. Add the same environment variables as above
6. Click "Create Static Site"

## 4. Admin Credentials Setup

**Important**: The admin credentials are managed by the backend. You'll need to:

1. Update your backend database/configuration with the new admin credentials:
   - **Email**: sujalparmar@gmail.com
   - **Password**: suj@l123

2. Ensure your backend API endpoints for admin authentication are configured correctly

## 5. Post-Deployment Checklist

- [ ] Test admin login with new credentials
- [ ] Verify all pages load correctly
- [ ] Test file upload functionality
- [ ] Check Firebase authentication works
- [ ] Verify API endpoints are accessible
- [ ] Test responsive design on mobile devices

## 6. Custom Domain (Optional)

### For Vercel:
1. Go to your project dashboard
2. Click "Settings" → "Domains"
3. Add your custom domain
4. Update DNS records as instructed

### For Render:
1. Go to your static site dashboard
2. Click "Settings" → "Custom Domains"
3. Add your domain and configure DNS

## Environment Variables Reference

Create a `.env` file in your project root with these variables:

```env
# API Configuration
VITE_API_BASE_URL=https://your-backend-url.com/api

# Firebase Configuration
VITE_FIREBASE_API_KEY=your_firebase_api_key
VITE_FIREBASE_AUTH_DOMAIN=your_project_id.firebaseapp.com
VITE_FIREBASE_PROJECT_ID=your_project_id
VITE_FIREBASE_STORAGE_BUCKET=your_project_id.appspot.com
VITE_FIREBASE_MESSAGING_SENDER_ID=your_messaging_sender_id
VITE_FIREBASE_APP_ID=your_app_id
VITE_FIREBASE_MEASUREMENT_ID=your_measurement_id
```

## Troubleshooting

### Common Issues:

1. **Build Fails**: Check that all dependencies are listed in package.json
2. **Environment Variables**: Ensure all required variables are set in deployment platform
3. **API Calls Fail**: Verify CORS settings and API URL configuration
4. **Firebase Auth Issues**: Check Firebase project configuration and API keys

### Support

For issues related to this deployment, contact: sujalparmar@gmail.com
