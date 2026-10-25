# Roy Music — Android prototype

This is a lightweight Android WebView starter app for a personal online music player. It lives alongside the ReVanced patch research in this repository; it is **not** a modified YouTube Music APK.

## Current prototype features

- Dark Home page where you add YouTube / YouTube Music links.
- Embedded YouTube playback when a video allows embedding.
- Local song-link list and recent-play records using WebView local storage.
- A `Repeted Song` tab placeholder.

## Limitations

- It cannot automatically clone YouTube Music's personalised recommendations; there is no unrestricted public API for that feed. Songs are added by pasting links.
- Automatic completed-play detection and automatic repeated-song playlist population are not implemented yet.
- It stores song IDs/links locally, **not audio files**. No YouTube audio extraction or offline playback.
- Some videos disallow embedding and must be opened in YouTube.
- No APK has been built or tested from this commit yet.

## Build in VS Code on Windows

Requirements: Android Studio/Android SDK, JDK 17, and Gradle 8.9 or compatible. This repo does not yet include the Gradle wrapper.

```powershell
cd D:\vscode\Android\yt-music-revanced-custom\android-player
gradle assembleDebug
```

If `gradle` is not on PATH, open the folder in Android Studio and sync with a compatible Gradle installation. The debug APK should be generated at `app\build\outputs\apk\debug\app-debug.apk` after a successful build.

## Next steps

1. Add Gradle wrapper and verify a clean build.
2. Add supported player state callbacks to track completed plays and populate `Repeted Song` after two qualifying plays within seven days.
3. Add 90-day cleanup for app-owned metadata/artwork cache only. Do not delete YouTube-managed cache or claim audio is retained.
4. Test playback, navigation, persistence and unsupported embeds on Android.
