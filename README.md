# NovaCash — Cashbook App

A login-protected cashbook app (deposit / cash-out tracking) built as a mobile
web app and packaged into an installable Android APK using Capacitor + GitHub Actions.

## How this works

- `www/index.html` — the actual app (login, register, forgot password, deposit/cashout, ledger)
- `capacitor.config.json` — tells Capacitor to wrap `www/` into a native Android app
- `.github/workflows/build-apk.yml` — a GitHub Actions workflow that automatically
  builds the `.apk` on GitHub's servers every time you push. **You don't need
  Android Studio or any Android SDK installed on your own computer.**

## One-time setup

1. Create a new **public or private** repository on GitHub (e.g. `novacash`).
2. Upload every file in this folder to that repo, keeping the same folder structure:
   ```
   novacash/
   ├── www/
   │   └── index.html
   ├── package.json
   ├── capacitor.config.json
   └── .github/
       └── workflows/
           └── build-apk.yml
   ```
   Easiest way: on GitHub, click **Add file → Upload files**, drag in the whole
   folder (GitHub preserves the folder structure), and commit to the `main` branch.

   Or, from a terminal with git installed:
   ```bash
   cd novacash-repo
   git init
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/YOUR_USERNAME/novacash.git
   git push -u origin main
   ```

3. As soon as you push, GitHub automatically starts the build. Go to your repo's
   **Actions** tab — you'll see a workflow run called "Build APK" in progress
   (takes about 2–4 minutes).

4. When it finishes (green checkmark), click into that run, scroll to
   **Artifacts**, and download **novacash-debug-apk**. It's a zip containing
   `app-debug.apk`.

5. Transfer `app-debug.apk` to your Android phone (via USB, Google Drive, email
   to yourself, etc.) and tap it to install. You may need to allow
   "Install unknown apps" for whichever app you used to open the file
   (Settings → Apps → Special access → Install unknown apps).

## Making changes later

Any time you edit `www/index.html` (colors, features, text) and push the
change to GitHub, the Actions workflow re-runs automatically and produces a
fresh APK in the same place — no local build tools needed.

## Notes

- This produces a **debug** APK, which is perfectly fine for installing on
  your own phone and testing. It won't be accepted by the Google Play Store
  as-is — that requires a signed **release** build, which is a further step
  if you ever want to publish it there.
- The app stores usernames, passwords (hashed), and transactions in the
  phone's local app storage — there's no cloud server, so data stays on that
  device only and won't sync across phones.
