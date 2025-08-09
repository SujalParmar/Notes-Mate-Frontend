# 🔥 Complete Firebase Setup Guide for Notes Mate

## Step 1: Create Firebase Account

### 1.1 Sign Up for Firebase
1. **Go to Firebase Console**: https://console.firebase.google.com/
2. **Sign in with Google**: Use your Google account (sujalparmar@gmail.com)
3. **Accept Terms**: Accept Firebase terms and conditions

## Step 2: Create a New Firebase Project

### 2.1 Create Project
1. **Click "Create a project"**
2. **Project Name**: Enter `notes-mate` (or any name you prefer)
3. **Project ID**: Firebase will auto-generate (e.g., `notes-mate-12345`)
4. **Analytics**: Choose "Enable Google Analytics" (recommended)
5. **Analytics Account**: Select your Google Analytics account or create new
6. **Click "Create project"**
7. **Wait for setup** (takes 1-2 minutes)
8. **Click "Continue"**

## Step 3: Configure Authentication

### 3.1 Enable Authentication
1. **In Firebase Console**, click on your project
2. **Left sidebar** → Click "Authentication"
3. **Click "Get started"**
4. **Go to "Sign-in method" tab**

### 3.2 Enable Google Sign-In
1. **Click on "Google"** in the sign-in providers list
2. **Toggle "Enable"** to ON
3. **Project support email**: Select `sujalparmar@gmail.com`
4. **Click "Save"**

### 3.3 Enable Email/Password Sign-In (for Admin)
1. **Click on "Email/Password"** in the sign-in providers list
2. **Toggle "Enable"** to ON
3. **Click "Save"**

### 3.4 Add Authorized Domains
1. **Go to "Settings" tab** in Authentication
2. **Authorized domains section**
3. **Add these domains**:
   - `localhost` (for development)
   - Your future domain name (for production)

## Step 4: Create Web App and Get API Keys

### 4.1 Register Web App
1. **Go to Project Overview** (home icon in sidebar)
2. **Click the "</>" icon** (Web app)
3. **App nickname**: Enter `notes-mate-web`
4. **Firebase Hosting**: Check this box (optional but recommended)
5. **Click "Register app"**

### 4.2 Get Firebase Configuration
After registering, you'll see a configuration object like this:

```javascript
const firebaseConfig = {
  apiKey: "AIzaSyC...",
  authDomain: "notes-mate-12345.firebaseapp.com",
  projectId: "notes-mate-12345",
  storageBucket: "notes-mate-12345.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abc123",
  measurementId: "G-ABC123DEF"
};
```

**IMPORTANT**: Copy this configuration - you'll need it for your .env file!

## Step 5: Set Up Firestore Database (Optional)

### 5.1 Create Firestore Database
1. **Left sidebar** → Click "Firestore Database"
2. **Click "Create database"**
3. **Security rules**: Choose "Start in test mode" (for development)
4. **Location**: Choose your region (e.g., us-central1)
5. **Click "Done"**

## Step 6: Configure Your Environment File

### 6.1 Create .env File
1. **Navigate to your project folder**:
   ```
   c:\Users\sujal\OneDrive\Desktop\Notes-mate\Notes-Mate-main\Notes-Mate-main
   ```

2. **Copy the example file**:
   ```powershell
   copy .env.example .env
   ```

3. **Edit the .env file** with your Firebase configuration:

```env
# API Configuration
VITE_API_BASE_URL=http://localhost:5000/api

# Firebase Configuration (Replace with your values)
VITE_FIREBASE_API_KEY=AIzaSyC...
VITE_FIREBASE_AUTH_DOMAIN=notes-mate-12345.firebaseapp.com
VITE_FIREBASE_PROJECT_ID=notes-mate-12345
VITE_FIREBASE_STORAGE_BUCKET=notes-mate-12345.appspot.com
VITE_FIREBASE_MESSAGING_SENDER_ID=123456789
VITE_FIREBASE_APP_ID=1:123456789:web:abc123
VITE_FIREBASE_MEASUREMENT_ID=G-ABC123DEF
```

## Step 7: Set Up Admin User

### 7.1 Create Admin User in Firebase
1. **Go to Authentication** → **Users tab**
2. **Click "Add user"**
3. **Email**: `sujalparmar@gmail.com`
4. **Password**: `suj@l123`
5. **Click "Add user"**

### 7.2 Set Custom Claims (Advanced)
For admin privileges, you might need to set custom claims. This typically requires backend code or Firebase Admin SDK.

## Step 8: Configure Storage (If Needed)

### 8.1 Set Up Firebase Storage
1. **Left sidebar** → Click "Storage"
2. **Click "Get started"**
3. **Security rules**: Choose "Start in test mode"
4. **Location**: Choose same region as Firestore
5. **Click "Done"**

### 8.2 Configure CORS for Storage
Add these rules in Storage → Rules:
```javascript
rules_version = '2';
service firebase.storage {
  match /b/{bucket}/o {
    match /{allPaths=**} {
      allow read, write: if request.auth != null;
    }
  }
}
```

## Step 9: Test Your Configuration

### 9.1 Verify Environment Variables
Create a test file to verify your configuration:

```javascript
// test-firebase.js
import { initializeApp } from 'firebase/app';

const firebaseConfig = {
  apiKey: process.env.VITE_FIREBASE_API_KEY,
  authDomain: process.env.VITE_FIREBASE_AUTH_DOMAIN,
  projectId: process.env.VITE_FIREBASE_PROJECT_ID,
  storageBucket: process.env.VITE_FIREBASE_STORAGE_BUCKET,
  messagingSenderId: process.env.VITE_FIREBASE_MESSAGING_SENDER_ID,
  appId: process.env.VITE_FIREBASE_APP_ID,
  measurementId: process.env.VITE_FIREBASE_MEASUREMENT_ID
};

const app = initializeApp(firebaseConfig);
console.log('Firebase initialized successfully!');
```

## Step 10: Security Configuration

### 10.1 Firestore Security Rules
```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Users can read/write their own data
    match /users/{userId} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
    
    // Admin can access everything
    match /{document=**} {
      allow read, write: if request.auth != null && 
        request.auth.token.email == 'sujalparmar@gmail.com';
    }
  }
}
```

## Step 11: Production Configuration

### 11.1 For Deployment
When deploying to Vercel/Render, add these environment variables:

```
VITE_API_BASE_URL=https://your-backend-url.com/api
VITE_FIREBASE_API_KEY=your_api_key
VITE_FIREBASE_AUTH_DOMAIN=your_project_id.firebaseapp.com
VITE_FIREBASE_PROJECT_ID=your_project_id
VITE_FIREBASE_STORAGE_BUCKET=your_project_id.appspot.com
VITE_FIREBASE_MESSAGING_SENDER_ID=your_messaging_sender_id
VITE_FIREBASE_APP_ID=your_app_id
VITE_FIREBASE_MEASUREMENT_ID=your_measurement_id
```

## 🔑 Summary of What You'll Get

After completing this setup, you'll have:

✅ **Firebase Project**: `notes-mate` project in Firebase Console  
✅ **Authentication**: Google Sign-in and Email/Password enabled  
✅ **API Keys**: All required configuration values  
✅ **Admin User**: sujalparmar@gmail.com with admin access  
✅ **Database**: Firestore database (optional)  
✅ **Storage**: Firebase Storage for file uploads  
✅ **Environment File**: .env configured with all keys  

## 🚨 Important Security Notes

1. **Never commit .env file** to Git (it's already in .gitignore)
2. **Keep API keys secure** - don't share them publicly
3. **Use environment variables** for production deployment
4. **Configure proper security rules** before going live

## 🆘 Troubleshooting

### Common Issues:
1. **API Key not working**: Double-check you copied the entire key
2. **Authentication fails**: Verify domain is in authorized domains
3. **CORS errors**: Check Firebase project configuration
4. **Admin access denied**: Ensure admin user is created with correct email

## 📞 Next Steps

After completing Firebase setup:
1. ✅ Test your .env configuration
2. ✅ Run `npm install` to install dependencies
3. ✅ Run `npm run dev` to start development server
4. ✅ Test Google authentication
5. ✅ Test admin login with sujalparmar@gmail.com

---

**Project Owner**: Sujal Parmar (sujalparmar@gmail.com)  
**Firebase Project**: notes-mate  
**Admin Email**: sujalparmar@gmail.com  
**Admin Password**: suj@l123
