# GitHub APK build

1. Upload this project to a GitHub repository.
2. Open **Actions**.
3. Select **Build Android APK**.
4. Choose **Run workflow**.
5. After the run succeeds, download the **telegram-forwarder-debug-apk** artifact.

The workflow installs Gradle in GitHub Actions, so the repository does not need `android/gradlew` or the Gradle wrapper JAR.

The APK contains the native Kotlin foreground service. No database or cloud backend is required.
