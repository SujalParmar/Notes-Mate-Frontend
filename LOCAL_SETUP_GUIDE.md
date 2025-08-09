# 🚀 Complete Local Setup Guide for Notes Mate

## Prerequisites Installation

### Step 1: Install Node.js and npm

1. **Download Node.js:**
   - Visit: https://nodejs.org/
   - Download the **LTS version** (Long Term Support)
   - Choose Windows Installer (.msi) for 64-bit

2. **Install Node.js:**
   - Run the downloaded installer
   - Accept all default settings
   - Ensure "Add to PATH" is checked
   - Restart your computer after installation

3. **Verify Installation:**
   ```powershell
   node --version
   npm --version
   ```
   You should see version numbers for both commands.

## Frontend Setup (React/Vite)

### Step 2: Install Frontend Dependencies

1. **Navigate to project directory:**
   ```powershell
   cd "c:\Users\sujal\OneDrive\Desktop\Notes-mate\Notes-Mate-main\Notes-Mate-main"
   ```

2. **Install all dependencies:**
   ```powershell
   npm install
   ```
   This will install all packages listed in package.json (React, Vite, etc.)

3. **Create environment file:**
   ```powershell
   copy .env.example .env
   ```

4. **Edit the .env file** with your Firebase configuration:
   ```env
   VITE_API_BASE_URL=http://localhost:5000/api
   VITE_FIREBASE_API_KEY=your_firebase_api_key
   VITE_FIREBASE_AUTH_DOMAIN=your_project_id.firebaseapp.com
   VITE_FIREBASE_PROJECT_ID=your_project_id
   VITE_FIREBASE_STORAGE_BUCKET=your_project_id.appspot.com
   VITE_FIREBASE_MESSAGING_SENDER_ID=your_messaging_sender_id
   VITE_FIREBASE_APP_ID=your_app_id
   VITE_FIREBASE_MEASUREMENT_ID=your_measurement_id
   ```

### Step 3: Start Frontend Development Server

```powershell
npm run dev
```

The frontend will start at: http://localhost:5173

## Backend Setup (If you have backend code)

### Step 4: Backend Setup

**Note:** This project appears to be frontend-only and connects to an external backend API. If you have the backend code separately:

1. **Navigate to backend directory:**
   ```powershell
   cd path\to\your\backend\folder
   ```

2. **Install backend dependencies:**
   ```powershell
   npm install
   ```

3. **Create backend .env file** with:
   ```env
   PORT=5000
   MONGODB_URI=your_mongodb_connection_string
   JWT_SECRET=your_jwt_secret
   FIREBASE_ADMIN_SDK_KEY=path_to_firebase_admin_key.json
   ```

4. **Start backend server:**
   ```powershell
   npm start
   # or
   npm run dev
   ```

## Firebase Setup

### Step 5: Configure Firebase

1. **Go to Firebase Console:**
   - Visit: https://console.firebase.google.com/
   - Create a new project or use existing one

2. **Enable Authentication:**
   - Go to Authentication → Sign-in method
   - Enable Google sign-in
   - Add your domain to authorized domains

3. **Get Firebase Config:**
   - Go to Project Settings → General
   - Scroll down to "Your apps"
   - Click "Web app" and copy the config
   - Update your .env file with these values

## Admin Credentials Setup

### Step 6: Configure Admin Access

**Important:** The admin credentials need to be set up in your backend database:

- **Admin Email:** sujalparmar@gmail.com
- **Admin Password:** suj@l123

If you're using a database (MongoDB/Firebase), you'll need to create an admin user with these credentials.

## Running the Complete Application

### Step 7: Start Both Servers

1. **Terminal 1 - Frontend:**
   ```powershell
   cd "c:\Users\sujal\OneDrive\Desktop\Notes-mate\Notes-Mate-main\Notes-Mate-main"
   npm run dev
   ```

2. **Terminal 2 - Backend (if you have it):**
   ```powershell
   cd path\to\backend
   npm start
   ```

### Step 8: Access the Application

- **Frontend:** http://localhost:5173
- **Backend API:** http://localhost:5000 (if running locally)

## Troubleshooting

### Common Issues:

1. **Node.js not recognized:**
   - Restart PowerShell after Node.js installation
   - Check if Node.js is in your PATH

2. **npm install fails:**
   - Try: `npm cache clean --force`
   - Then: `npm install`

3. **Port already in use:**
   - Frontend: The dev server will automatically use the next available port
   - Backend: Change PORT in .env file

4. **Firebase errors:**
   - Check if all Firebase config values are correct
   - Ensure Firebase project is properly configured

### Getting Help

If you encounter issues:
1. Check the browser console for errors (F12)
2. Check terminal output for error messages
3. Verify all environment variables are set correctly

## Next Steps After Setup

1. Test the application in your browser
2. Try logging in with Google authentication
3. Test admin login with the new credentials
4. Upload a test note to verify functionality

---

**Project Owner:** Sujal Parmar (sujalparmar@gmail.com)
**Admin Access:** sujalparmar@gmail.com / suj@l123
