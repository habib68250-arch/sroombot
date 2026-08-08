# Telegram Message Forwarder (Android Native Background Service)

A complete Android application built with React, TypeScript, Capacitor, and Native Kotlin Foreground Service that automatically forwards incoming messages from your Telegram Bot directly to a specified Telegram Group.

**No Cloud Server Required. No External Backend. No Database.** Everything runs directly on your Android device using official Telegram Bot API long polling.

---

## 🌟 Key Features

- 📱 **100% On-Device Execution**: Runs directly on your Android phone — zero cloud server or database needed.
- ⚡ **Native Android Foreground Service**: Continues running reliably in the background when the app is minimized, screen is locked, or other apps are in use.
- 🔒 **Encrypted Local Storage**: Bot tokens are stored securely on your device using Android `EncryptedSharedPreferences` (AES-256).
- 🔄 **Auto Start on Boot**: Optional setting to automatically launch the Telegram forwarding service when your phone restarts.
- 💬 **Complete Telegram Media Support**: Uses Telegram Bot API's `copyMessage` method to copy Text, Photos, Videos, Documents, Voice Notes, Audio, Stickers, Animations, Polls, and Locations.
- 🔔 **Status Notification Drawer**: Displays a persistent low-priority status notification ("Telegram Forwarder is running") with a quick "Stop" button in the notification shade.
- 🛠️ **GitHub Actions Automated Build**: Built-in `.github/workflows/build-android.yml` installs Gradle in CI and compiles the debug APK automatically. No Gradle wrapper is required in the repository.

---

## 🚀 Step-by-Step Setup Guide

### Step 1: Create your Telegram Bot & Get Token
1. Open Telegram and search for `@BotFather`.
2. Send command `/newbot`.
3. Follow the prompts to set a display name and username for your bot.
4. `@BotFather` will give you an HTTP API Token (e.g. `123456789:ABCxxxxxxxxxxxxxxxx`). **Save this token.**

### Step 2: Set Up Target Telegram Group
1. Open your Target Telegram Group.
2. Add your new bot as a member of the group.
3. Promote your bot to **Administrator** with permission to post/send messages.
4. Get your Group ID:
   - Add `@myidbot` or `@RawDataBot` to your group.
   - It will reply with the Group ID starting with `-100` (e.g., `-1001234567890`).
   - Remove `@myidbot` from the group after obtaining the ID.

---

## 📦 How to Build the APK on GitHub Actions

You don't need Android Studio installed locally! GitHub Actions will compile the Android APK for you:

1. **Upload Code to GitHub**:
   ```bash
   git init
   git add .
   git commit -m "Initial commit of Telegram Forwarder"
   git branch -M main
   git remote add origin https://github.com/YOUR_USERNAME/telegram-forwarder.git
   git push -u origin main
   ```

2. **Download Generated APK**:
   - Go to your repository on GitHub.
   - Click the **Actions** tab.
   - Select the latest workflow run ("Build Android APK").
   - Scroll down to **Artifacts** and download `app-debug.apk`.
   - Install `app-debug.apk` on your Android phone!

---

## 📱 Running the App on Android

1. Open **Telegram Forwarder** on your phone.
2. Enter your **Bot Token** and **Target Group ID**.
3. Tap **Test Connection** to verify your token and group accessibility.
4. Tap **Start Forwarding**.
5. The status indicator will turn green ("● Running in Background") and a persistent notification will appear in your notification bar.
6. You can now lock your screen or close the app UI. Incoming messages sent to your bot will automatically copy to your target group!

---

## 🔋 Disabling Android Battery Optimization

To prevent Android OS from putting the background process to sleep on certain manufacturers:

- **Samsung (OneUI)**: Settings → Apps → Telegram Forwarder → Battery → Set to **Unrestricted**.
- **Xiaomi / POCO (MIUI / HyperOS)**: Settings → Apps → Manage Apps → Telegram Forwarder → Enable **Autostart** & set Battery Saver to **No restrictions**.
- **OPPO / Realme (ColorOS)**: Settings → App Management → Telegram Forwarder → Allow **Auto-launch** & Background activity.
- **Google Pixel / Stock Android**: Settings → Apps → Telegram Forwarder → App battery usage → Set to **Unrestricted**.

---

## 📂 Project Architecture

```
/
├── .github/workflows/
│   └── build-android.yml         # GitHub Actions workflow for compiling APK
├── android/                      # Native Android Project
│   ├── app/src/main/java/com/telegram/forwarder/
│   │   ├── TelegramForegroundService.kt # Native Kotlin Foreground Service for Long Polling
│   │   ├── BootReceiver.kt              # BroadcastReceiver for boot auto-start
│   │   ├── TelegramServicePlugin.kt     # Capacitor Plugin bridge
│   │   └── MainActivity.kt              # Main Capacitor Activity
│   └── app/src/main/AndroidManifest.xml
├── src/
│   ├── components/               # React UI Components
│   │   ├── Header.tsx
│   │   ├── ConfigCard.tsx
│   │   ├── DashboardStats.tsx
│   │   ├── SettingsSection.tsx
│   │   └── LogTerminal.tsx
│   ├── services/
│   │   └── telegramServiceBridge.ts     # Native & Web service bridge
│   └── App.tsx
├── capacitor.config.json         # Capacitor configuration
└── README.md
```

---

## 🔒 Security & Privacy

- **No Remote Loggers**: Bot tokens and messages are never transmitted to any third-party analytics or external server.
- **Direct Telegram Communication**: The app connects exclusively to official Telegram Bot API endpoints (`https://api.telegram.org`).
- **Encrypted Storage**: Credentials are saved using Android `EncryptedSharedPreferences` backed by Android Keystore System.

---

## 📄 License

Apache-2.0 License. Free for personal and commercial use.
