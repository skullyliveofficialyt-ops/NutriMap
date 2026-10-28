# Nutrimap: desktop + mobile apps

One web app in `www/`, packaged for Windows, macOS, Linux (Electron) and Android / iOS (Capacitor).

## Fastest way: let GitHub build everything (no tools to install)
1. Create a free account at github.com and a new repository.
2. Upload every file and folder from this project (including the hidden `.github` folder), or push with git, to the `main` branch.
3. Open the **Actions** tab. The "Build Nutrimap apps" workflow starts by itself (or press **Run workflow**).
4. After 10 to 20 minutes, open the finished run and download from **Artifacts**:
   - `nutrimap-desktop-windows-latest`: Windows installer (.exe)
   - `nutrimap-desktop-macos-latest`: Mac disk image (.dmg)
   - `nutrimap-desktop-ubuntu-latest`: Linux AppImage
   - `nutrimap-android-apk`: Android app (debug APK) you can install on a phone

Installing the files:
- **Windows:** Windows may warn about an unknown publisher because the app isn't code-signed. Choose More info > Run anyway.
- **Mac:** the app isn't signed or notarized. Right-click the app and choose Open the first time.
- **Android:** allow "install unknown apps" for your browser or file manager, then open the APK.
- **iPhone:** iOS apps can't be built this way. They need a Mac with Xcode and an Apple Developer account (see below).

## Build on your own computer instead
Needs Node.js 18+.
```
npm install
npm run desktop            # run the desktop app
npm run desktop:win        # or desktop:mac / desktop:linux (build on that OS)
npx cap add android        # then: npm run mobile:sync && npm run mobile:android
npx cap add ios            # Mac only, then: npm run mobile:sync && npm run mobile:ios
```
Edit anything in `www/`, then run `npm run mobile:sync` to update the mobile projects.

## Before publishing to a store
- Change `appId` (`com.nutrimap.app`) in `package.json` and `capacitor.config.json` to one you own, like `com.yourname.nutrimap`. It can't be changed after you publish.
- Google Play needs a signed release build (Android Studio: Build > Generate Signed Bundle). The CI build above is a debug APK for testing.
- App Store needs an Apple Developer account and a Mac.
- Dependencies are set to `latest`. After your first successful build, commit the generated `package-lock.json` so future builds use the same versions.

## Notes
- Food data lives in the `F` array in `www/index.html`. Values are approximate averages.
- Logs are saved on each device. Use the **Backup** button in the app to copy or save your data and restore it elsewhere.
