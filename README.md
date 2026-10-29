# Financial Tracker

A simple personal money tracker that runs in your phone or desktop browser. Record **money in** and **money out**, see your balance at any time, and print reports by month, year, or since day one. Your data is saved automatically to **your own Google Drive**, and it works offline.

## Features

- **Money In** (green) and **Money Out** (orange to red) with a running balance
- Types for each entry (ATM, Salary, Gift, Food, Transport, Bills, Shopping, Other) and an optional note
- **Reports** by month, year, or since day one: balance brought forward, total in, total out, balance at end, spending by type, and all entries
- **Print or save as PDF** from the Report tab
- **Works offline**: entries are saved on the device first and uploaded to Google Drive when the internet returns
- **Installable** on a phone like an app (Add to Home Screen)
- No server and no database. Your data lives in one file in your Drive: `my-money-data.json`

## Files

| File | Purpose |
|------|---------|
| `index.html` | The whole app (interface and logic) |
| `sw.js` | Lets the app open offline |
| `manifest.webmanifest` | Lets the app be installed on a phone |
| `icon-192.png`, `icon-512.png` | App icons |

## Setup

### 1. Publish the app (GitHub Pages)

1. Upload all files to this repository.
2. Go to **Settings > Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**, select the `main` branch and the `/ (root)` folder, then click **Save**.
4. After a minute, your link appears, like `https://YOUR-USERNAME.github.io/Financial-Tracker/`.

### 2. Connect Google Drive

1. Open [Google Cloud Console](https://console.cloud.google.com) and create a new project.
2. Go to **APIs & Services > Library**, search for **Google Drive API**, and click **Enable**.
3. Go to **APIs & Services > OAuth consent screen**. Choose **External**, fill in the app name and your email, and save. While the app is in *Testing* mode, add your own Gmail address under **Test users**.
4. Go to **APIs & Services > Credentials > Create credentials > OAuth client ID**.
   - Application type: **Web application**
   - Authorized JavaScript origins: your site address, for example `https://YOUR-USERNAME.github.io` (no path at the end, no trailing slash)
5. Copy the **Client ID**.
6. Open `index.html`, find this line near the top of the script, and paste your Client ID:

   ```js
   const CLIENT_ID='PASTE_YOUR_GOOGLE_CLIENT_ID_HERE';
   ```
7. Commit the change. Wait a minute for GitHub Pages to update.

### 3. Install on your phone

1. Open your link in Chrome (Android) or Safari (iPhone).
2. Tap the status button at the top right (it says **Connect Drive**) and sign in with Google. Allow access to files this app creates.
3. Install it:
   - **Android (Chrome):** menu > **Install app** or **Add to Home screen**
   - **iPhone (Safari):** Share > **Add to Home Screen**

## How to use

1. Tap **+ Money In** when money comes in (ATM withdrawal, salary, gift). Enter the amount and save.
2. Tap **− Money Out** when you spend. Pick a type and save.
3. Your balance updates immediately. Example: 100,000 in, then 10,000 out for food gives 90,000. Another 100,000 in gives 190,000.
4. Open the **Report** tab, choose Month, Year, or Since day one, and tap **Print or save as PDF**.
5. To remove a mistake, tap the **×** next to an entry in History.

## Sync and offline

- Every entry is saved on the device first, so you can add entries with no internet.
- When the device is online, the app downloads the file from Drive, merges it with what is on the device, and uploads the result. If you use two devices, entries from both are kept.
- The status button at the top shows the state: *Saved to Drive*, *Offline, will sync*, or *Tap to reconnect Drive*. If it asks you to reconnect, tap it and sign in again.
- Do not clear browser data while entries are still waiting to sync, because they would be lost.

## Settings

- **Currency:** change `const CUR='TSh';` at the top of the script in `index.html`.

## Privacy

- The app only requests the `drive.file` permission, so it can see only the file it creates, not the rest of your Drive.
- There is no server. Your data is stored on your device and in your own Google Drive.

## Troubleshooting

| Problem | Fix |
|---------|-----|
| Google sign-in says "access blocked" or "origin mismatch" | Check that your site address is listed under Authorized JavaScript origins, and that your Gmail is added as a Test user |
| Status says **Local only** | The Client ID was not pasted into `index.html` |
| Changes to the app do not show | Close and reopen the app, or clear the site data once |
| Status keeps saying **Tap to reconnect Drive** | Tap it and sign in again. Google sign-in expires after about an hour |

## Ideas for later

- Business version with separate books per person
- Categories you can edit
- Charts for spending by month
