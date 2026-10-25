# Feature specification: 90-day history/cache and repeat-playlist helper

## User goal

Reduce repeated network usage and automatically collect songs that are played to completion repeatedly.

## Intended behavior

### A. Cache-age tracking

- Record a stable track/video ID and the date/time when an app-owned cache entry is created.
- Expire app-owned cache entries at 90 days and remove only files this feature explicitly owns and can safely identify.
- Do not delete user-saved links, playlists, or unrelated app cache.
- The current prototype expires local play-history records after 90 days. It does not yet cache audio or implement an artwork-file cache.
- If the app's own cache cannot be safely controlled through a supported API, show this limitation and do not pretend the 90-day retention policy is active for that cache.

### B. “Repeted Song” playlist

- Playlist display name: `Repeted Song` (preserve the user's requested spelling).
- A qualifying completion is an embedded-player ENDED event for a video at least 30 seconds long with reported playback position at or above 90% of duration.
- When the same track has at least 2 qualifying completed plays in a rolling 7-day window, add it to the local playlist.
- Add each track only once; use a stable video ID rather than title text to avoid duplicates.
- Persist play timestamps locally so counts survive app restarts.
- If the feature cannot create or modify a YouTube Music playlist through a supported API, use a clearly labelled local playlist/list instead of claiming it synced to the user's account.

## Important technical constraints

YouTube Music is proprietary, and the normal ReVanced patching project does not include its source code. Its streaming cache is managed internally by the app and Android; cached audio may be evicted, encrypted, segmented, or tied to expiring stream URLs. A patch must not assume it can keep an MP3 file for 90 days or replay it offline just because a cache entry exists.

The prototype uses the official YouTube embedded player API for playback callbacks where available. Those callbacks require device testing and may not work for every video. The prototype does not download/extract YouTube audio, bypass access controls, or provide offline playback.

## Acceptance tests

- A skipped track does not count unless the player reports an end event and position is at least 90%.
- Two qualifying completed plays of the same track within 7 days add it once.
- A third qualifying play does not create a duplicate playlist entry.
- Completed plays older than the rolling 7-day window do not count toward the threshold.
- Local play-history records older than 90 days are pruned.
- App restart does not erase locally stored play timestamps.
- Unsupported player or cache hooks fail safely and are clearly documented.

## Status

Prototype logic has been added to `android-player/app/src/main/assets/index.html`; it has not yet been built or tested on a device. Actual audio caching and offline playback remain unimplemented.
