# C25K Buddy - Wear OS App

A dead-simple Wear OS companion app for the Couch to 5K (C25K) running program. C25K switches between running and walking to help build up to a point where you can run a 5K. Your watch will vibrate once when you need to walk and twice when you need to run. This helps you do your run without carrying a phone or staring at a screen. You can also use this app to track your progess with the program locally (all data is stored in your watch only).

This app was only made as a weekend project for a Galaxy Watch 5.

Couch To 5K plan is taken from this NHS PDF: https://digitalcampaignsstorage.blob.core.windows.net/campaigns-cms-prod/documents/c25k_printable_plan.pdf

### Key Features
- C25K program schedule tracking
- Workout progress persistence
- Real-time workout guidance with watch vibrations
- Progress visualization during workout

## Screenshots
<img width="459" alt="image" src="https://github.com/user-attachments/assets/3ffab5c0-b080-427a-8fe6-519ce2972839" />

<img width="459" alt="image" src="https://github.com/user-attachments/assets/9a4f6be0-27d1-424f-a556-681f7f7598c4" />

<img width="459" alt="image" src="https://github.com/user-attachments/assets/201a666f-27f3-4791-bbb3-8be6f146a200" />

<img width="456" alt="image" src="https://github.com/user-attachments/assets/5b68340d-492d-49df-89ca-57fbae1ab09a" />

<img width="456" alt="image" src="https://github.com/user-attachments/assets/4cc0d28b-82ce-4465-a020-a6fd4cbea9d3" />

### 

## Prerequisites

Before you begin, ensure you have the following installed:

1. **Android Studio** with:
   - Android SDK Platform 35
   - Android SDK Build-Tools
   - Android SDK Command-line Tools
2. **Java Development Kit (JDK) 11** (as specified in build.gradle.kts)
3. **ADB (Android Debug Bridge)** installed and in your PATH
4. **A Wear OS device** with:
   - Minimum SDK version 30 (Wear OS 3.0)
   - Developer options enabled
   - ADB debugging enabled
   - Wireless debugging enabled (for wireless deployment)

## Building the Project

1. Clone the repository:

2. Create a keystore for signing the release build:
   ```bash
   keytool -genkey -v -keystore c25k-release-key.keystore -alias c25kbuddy -keyalg RSA -keysize 2048 -validity 10000
   ```

3. Set up your keystore credentials (either in environment variables or gradle.properties):
   ```bash
   # Option 1: Environment variables
   export KEYSTORE_PASSWORD="your_keystore_password"
   export KEY_PASSWORD="your_key_password"

   # Option 2: Add to gradle.properties
   keystore.password=your_keystore_password
   key.password=your_key_password
   ```

4. Build the release APK:
   ```bash
   ./gradlew :wear:assembleRelease
   ```

The release APK will be located at:
```
wear/build/outputs/apk/release/wear-release.apk
```

## Deploying to Your Watch

### Wireless Deployment (Recommended)

1. Enable Developer Options on your watch:
   - Go to Settings > System > About
   - Tap "Build number" 7 times
   - Enter your watch's PIN if prompted

2. Enable ADB Debugging:
   - Go to Settings > Developer options
   - Enable "ADB debugging"
   - Enable "Wireless debugging"

3. Connect your watch to your computer:
   ```bash
   # Get your watch's IP address and port from the Wireless debugging screen
   adb connect <watch_ip>:<port>
   ```

4. Verify the connection:
   ```bash
   adb devices
   # You should see your watch listed
   ```

5. Install the app:
   ```bash
   adb install -r wear/build/outputs/apk/release/wear-release.apk
   ```

### USB Deployment (Alternative)

1. Connect your watch to your computer via USB
2. Enable USB debugging in Developer options
3. Install the app:
   ```bash
   adb install -r wear/build/outputs/apk/release/wear-release.apk
   ```

## Troubleshooting

### Common Issues

1. **ADB Connection Issues**
   - Ensure your watch and computer are on the same network
   - Try disabling and re-enabling wireless debugging
   - Restart ADB server: `adb kill-server && adb start-server`

2. **Build Failures**
   - Ensure all prerequisites are installed
   - Try cleaning the project: `./gradlew clean`
   - Check that your keystore credentials are correctly set

3. **Installation Failures**
   - Ensure your watch has enough storage space
   - Try uninstalling any previous versions: `adb uninstall com.example.c25kbuddy`
   - Check that your watch is compatible (requires Wear OS 3.0 or later)

## License

This project is licensed under the MIT License - see the LICENSE file for details. Feel free to do whatever you want with it.
