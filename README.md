# Scrapheap Tycoon — Android build

## Get your APK (no local setup — recommended)
1. Create a new empty repo on https://github.com (public or private).
2. Push this whole folder to it:
   ```
   git init
   git add .
   git commit -m "Scrapheap Tycoon"
   git branch -M main
   git remote add origin <your-repo-url>
   git push -u origin main
   ```
3. Go to your repo's "Actions" tab on GitHub. A build will run automatically (~3-5 min).
4. Open the finished run, scroll to "Artifacts", download `scrapheap-tycoon-debug-apk`.
5. Unzip it — inside is `app-debug.apk`. Copy that to your Android phone and tap it to install
   (you'll need to allow "install unknown apps" once).

This produces a DEBUG apk — fine for testing on your own phone right now. Before uploading to
the Play Store you need a signed RELEASE build (see below).

## Building locally instead (Android Studio)
Open the `android/` folder directly in Android Studio → Build → Build Bundle(s)/APK(s) → Build APK(s).

## Before publishing to Play Store
- Replace the placeholder app icon (`android/app/src/main/res/mipmap-*`) with real artwork —
  required, and emoji placeholders won't pass review well.
- Generate a signing key and build a signed **release** AAB (Play Store requires AAB, not APK,
  for new apps): `keytool -genkey -v -keystore release-key.jks -keyalg RSA -keysize 2048 -validity 10000 -alias scrapheap`
  then `./gradlew bundleRelease`.
- Set `applicationId` in `android/app/build.gradle` if you want a different package name.
- Write a privacy policy (required even for simple games) and host it anywhere public.
- Register a Google Play Console developer account ($25 one-time).
