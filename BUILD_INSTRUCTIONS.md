# DOT WAR BATTLEZONE — Build APK Guide

## OPTION A: Android Studio (Easiest, Recommended)

1. Download **Android Studio** FREE from: https://developer.android.com/studio
2. Install it (takes ~5 min)
3. Open Android Studio → "Open Existing Project"
4. Select the `battlezone-apk` folder
5. Wait for Gradle sync (~2 min first time)
6. Click **Build → Build Bundle(s)/APK(s) → Build APK(s)**
7. APK saved to: `app/build/outputs/apk/debug/app-debug.apk`
8. Transfer to phone → Install ✅

---

## OPTION B: Online Build (No Setup Needed)

### Using Appetize / BuildAPK Online:
1. Zip the whole `battlezone-apk` folder
2. Upload to: https://www.jdeploy.com OR https://buildapps.online
3. Download the APK

### Using GitHub + CI/CD:
1. Create free account at https://github.com
2. Create new repo, upload all files from this folder
3. Add this to `.github/workflows/build.yml`:

```yaml
name: Build APK
on: [push]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-java@v3
        with:
          distribution: 'zulu'
          java-version: '17'
      - uses: android-actions/setup-android@v2
      - run: chmod +x gradlew && ./gradlew assembleDebug
      - uses: actions/upload-artifact@v3
        with:
          name: app-debug
          path: app/build/outputs/apk/debug/app-debug.apk
```
4. Push code → GitHub Actions builds APK → Download from Actions tab ✅

---

## OPTION C: Command Line (If you have Java)

```bash
# Install Android SDK command line tools, then:
chmod +x gradlew
./gradlew assembleDebug
# APK → app/build/outputs/apk/debug/app-debug.apk
```

---

## Install APK on Phone

1. Enable **Unknown Sources**: Settings → Security → Allow Unknown Sources
2. Copy APK to phone via USB or Google Drive
3. Tap APK file → Install
4. Find "DOT WAR BATTLEZONE" in your app drawer ✅

---

## Upload to Websites

- **Google Play Store**: https://play.google.com/console (needs $25 one-time fee)
- **APKPure**: https://apkpure.com/developer (free)
- **itch.io**: https://itch.io (free, great for indie games)
- **APKMonk**: https://www.apkmonk.com (free)
