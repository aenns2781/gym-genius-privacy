# Gym Genius Authentication Pages

This repository contains the privacy policy and authentication fallback pages for the Gym Genius mobile application. These pages are served using GitHub Pages.

## Purpose

This repository has two main purposes:

1. Host the Gym Genius privacy policy
2. Provide fallback authentication pages for processes like password reset and email change

## Authentication Pages

The authentication fallback pages are designed to handle deep links for the Gym Genius app. These pages attempt to redirect users back to the app using the `gym-genius://` URL scheme.

### How It Works

1. The app's authentication emails (password reset, email change) point to these GitHub Pages URLs
2. When a user clicks a link in an email, they land on these pages
3. The page automatically attempts to open the Gym Genius app with the appropriate tokens
4. If opening the app fails, the user sees instructions on how to complete the process manually

## Setup Steps

1. Update your GitHub username in the redirect URLs:
   - Replace `your-github-username` with your actual GitHub username in:
     - `frontend/app/auth/login.tsx`
     - `frontend/app/(app)/settings.tsx`

2. Set up iOS deep linking:
   - Add `gym-genius` as a URL scheme in your iOS app's Info.plist:
   ```xml
   <key>CFBundleURLTypes</key>
   <array>
     <dict>
       <key>CFBundleURLSchemes</key>
       <array>
         <string>gym-genius</string>
       </array>
     </dict>
   </array>
   ```

3. Set up Android deep linking:
   - Add intent filters in Android's AndroidManifest.xml:
   ```xml
   <intent-filter>
     <action android:name="android.intent.action.VIEW" />
     <category android:name="android.intent.category.DEFAULT" />
     <category android:name="android.intent.category.BROWSABLE" />
     <data android:scheme="gym-genius" />
   </intent-filter>
   ```

## Testing

To test the fallback pages:

1. Host these pages on GitHub Pages
2. Generate a test password reset or email change link
3. Click the link on a device with the Gym Genius app installed
4. The app should open automatically
5. Test without the app installed to verify the fallback instructions work

### Local Testing

You can test locally by:

1. Using a local HTTP server: `npx http-server ./gym-genius-privacy`
2. Opening `http://localhost:8080/auth/reset-password?token=test-token`
3. Opening `http://localhost:8080/auth/email-change?email=test@example.com&token=test-token`

## Customization

Update the following to customize for your needs:

- Replace references to `your-github-username` with your actual GitHub username
- Update styling to match your app's branding
- Modify the deep linking URL paths if your app uses different routes 