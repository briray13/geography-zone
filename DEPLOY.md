# Geography Zone — Deployment Guide

## What's in this folder

| File/Folder | Purpose |
|---|---|
| `index.html` | The full game — PWA-ready |
| `manifest.json` | PWA manifest (name, icons, theme) |
| `sw.js` | Service worker (offline support) |
| `icons/` | App icons for all devices |
| `favicon.ico` | Browser tab icon |
| `.nojekyll` | Tells GitHub Pages not to process files |
| `.github/workflows/deploy.yml` | Auto-deploy to GitHub Pages on every push |
| `capacitor-project/` | Native iOS & Android wrapper (Capacitor) |

---

## Step 1 — Publish as a free web app (GitHub Pages)

This takes about 10 minutes and gives you a public URL like `https://yourusername.github.io/geography-zone`.

1. Go to [github.com](https://github.com) and create a free account if you don't have one
2. Click **New repository** → name it `geography-zone` → set it to **Public** → click **Create repository**
3. Upload all files from this folder into the repo (drag & drop in the GitHub UI, or use GitHub Desktop)
4. Go to **Settings → Pages** → under *Source* select **GitHub Actions** → Save
5. The site deploys automatically. Your URL will be shown in the Pages settings.

> Every time you update a file and push it, the site redeploys automatically in ~30 seconds.

---

## Step 2 — Make it installable on phones (PWA — already done)

Once hosted, users on Android can tap **"Add to Home Screen"** in Chrome and it installs like a native app.

On iPhone/Safari: tap the Share button → **Add to Home Screen**.

The service worker caches everything so it works fully offline after the first visit.

---

## Step 3 — Publish to Google Play Store

**Requirements:** Google Play Developer account ($25 one-time fee at play.google.com/console)

1. Install [Android Studio](https://developer.android.com/studio) on your computer
2. Open `capacitor-project/` in a terminal and run:
   ```bash
   npx cap open android
   ```
3. Android Studio opens. Go to **Build → Generate Signed Bundle/APK**
4. Create a keystore (follow the wizard — save the keystore file safely, you'll need it forever)
5. Build the **Android App Bundle (.aab)**
6. Upload the `.aab` file to Google Play Console → create a new app → follow submission steps

---

## Step 4 — Publish to Apple App Store

**Requirements:** Apple Developer Program ($99/year at developer.apple.com) + a Mac with Xcode

1. On your Mac, open `capacitor-project/` in Terminal and run:
   ```bash
   npx cap open ios
   ```
2. Xcode opens. Select your Apple Developer Team in **Signing & Capabilities**
3. Update the Bundle Identifier if needed (currently `com.geographyzone.app`)
4. Go to **Product → Archive**
5. In the Organizer window, click **Distribute App → App Store Connect**
6. Follow prompts to upload, then go to [App Store Connect](https://appstoreconnect.apple.com) to complete the listing

---

## App details (for store listings)

- **App name:** Geography Zone
- **Bundle ID:** com.geographyzone.app
- **Category:** Education / Trivia
- **Age rating:** 4+ (no objectionable content)
- **Description:** Test your knowledge of world flags, capitals, and maps. 193 countries. Three quiz modes. Free.
