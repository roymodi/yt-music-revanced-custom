# Roy Music — Android prototype

This is a lightweight Android WebView starter app for a personal online music player. It lives alongside the ReVanced patch research in this repository; it is **not** a modified YouTube Music APK.

## Current prototype features

- Dark Home page where you add YouTube / YouTube Music links.
- YouTube embedded playback using the YouTube IFrame Player API when a video allows embedding.
- Song-link list with YouTube thumbnails, stored locally in WebView local storage.
- Recently Played list based on playback-start events.
- Local `Repeted Song` playlist: records a qualifying ended event when the player reports at least 90% of a video of 30 seconds or longer; adds the song after two qualifying completions in a rolling seven-day window.
- Removes local play-history records older than 90 days and completed-play counters outside the seven-day window.

## Limitations

- It cannot automatically clone YouTube Music's personalised Home recommendations; there is no unrestricted public API for that feed. Songs are added by pasting links.
- The repeated-play logic relies on YouTube's embedded player callbacks and has not yet been device-tested. Skipping near the end may be rejected if the reported playback position is below 90%, but player callbacks are not a tamper-proof proof of listening.
- The 90-day rule currently applies to this app's local play-history records, **not** YouTube's own audio cache or saved song links.
- This app stores song IDs, links, titles and playback history, not audio files. No YouTube audio extraction or offline playback is included.
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
2. Test player callbacks and playback persistence on an Android device.
3. Add a supported source for Home recommendations if one is available; do not scrape private endpoints.
4. Add 90-day cleanup for app-owned artwork/metadata cache only if implemented. Do not delete YouTube-managed cache or claim audio is retained.
