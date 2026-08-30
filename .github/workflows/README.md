# Real Android App Usage Tracker

This directory contains the complete native Android project implementing real app usage tracking with Android's `UsageStatsManager` and `UsageEvents`.

## Architecture & Real Android APIs
- **Permissions**: `android.permission.PACKAGE_USAGE_STATS` (system Usage Access permission) and `android.permission.QUERY_ALL_PACKAGES`.
- **Usage Statistics Engine**: `UsageStatsHelper.kt` queries `UsageStatsManager.queryEvents()` from midnight to now, reconstructing exact foreground/background intervals and launch counts without synthetic data.
- **Package Manager Integration**: Resolves installed app labels and base64 app icons directly from the device's installed packages.
- **Native Bridge (`UsageBridge.kt`)**: Provides the JavaScript interface `@JavascriptInterface` (`AndroidUsageStats`) to feed real usage data directly to the user interface.
- **Privacy First**: 100% on-device processing. No data is sent to external servers or cloud services.

## How to Build the APK

### Method 1: Android Studio
1. Open Android Studio.
2. Select **Open** and select the `/android` folder from this repository.
3. Build the web assets into `android/app/src/main/assets` (`npm run build`).
4. Click **Build > Build Bundle(s) / APK(s) > Build APK(s)**.
5. Transfer the generated `app-debug.apk` to your real Android phone and install it.

### Method 2: Command Line (Gradle)
```bash
cd android
./gradlew assembleDebug
```
The APK will be generated at:
`android/app/build/outputs/apk/debug/app-debug.apk`

## Granting Usage Access on Your Device
When you launch the app on your Android device:
1. Tap the **Grant Usage Access** button.
2. The app will open Android System Settings (**Usage Access**).
3. Find **App Usage Tracker** in the list and toggle **Permit usage access** to ON.
4. Return to the app — your actual device usage will load instantly!
