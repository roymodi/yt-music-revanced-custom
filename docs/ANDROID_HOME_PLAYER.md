# Android Home page music player

The prototype is in [android-player](../android-player/README.md).

## Home page behavior

- Users paste a YouTube / YouTube Music link.
- The app stores the video ID and link locally and lists it on Home.
- Selecting a row opens the embedded YouTube player.
- The first prototype stores local play-launch history, not confirmed completed plays.

## Official Home feed limitation

YouTube Music's personalised Home feed and full catalogue are not exposed through an unrestricted public API. Do not scrape private endpoints or claim static entries are live recommendations. A future implementation can use supported APIs or user-supplied links.

## Cache policy

Only app-owned metadata and artwork can be expired safely by this app. The prototype stores song IDs and links locally. Actual audio caching/offline playback is not implemented; it must use an authorised playback/offline mechanism.
