# Feature specification: 90-day cache and repeat-playlist helper

## User goal

Reduce repeated network usage and automatically collect songs that are played to completion repeatedly.

## Intended behavior

### A. Cache-age tracking

- Record a stable track/video ID and the date/time when a cache entry is first observed or created.
- Keep a cache-age record per track.
- Expire entries at 90 days and remove only files that this feature explicitly owns and can safely identify.
- Do not delete user downloads, playlists, listening history, or unrelated app cache.
- If the app's own cache cannot be safely controlled through the supported patch API, show this limitation and do not pretend the 90-day retention policy is active.

### B. “Repeted Song” playlist

- Playlist display name: `Repeted Song` (preserve the user's requested spelling).
- Count a play only when playback reaches the track's completion threshold; a reasonable initial threshold is at least 90% of duration, with a minimum duration check to avoid counting skips.
- When the same track has at least 2 qualifying completed plays in a rolling 7-day window, add it to the playlist.
- Add each track only once; use a stable track ID rather than title text to avoid duplicates.
- Persist play timestamps locally so counts survive app restarts.
- If the feature cannot create or modify a YouTube Music playlist through a supported API, use a clearly labelled local playlist/list instead of claiming it synced to the user's account.

## Important technical constraints

YouTube Music is proprietary, and the normal ReVanced patching project does not include its source code. Its streaming cache is managed internally by the app and Android; cached audio may be evicted, encrypted, segmented, or tied to expiring stream URLs. A patch must not assume it can keep an MP3 file for 90 days or replay it offline just because a cache entry exists.

The reliable first implementation should focus on completion-event detection, local play timestamps, deduplication, and a local “Repeted Song” list. Cache retention should be implemented only if a supported, version-compatible hook can identify and manage the relevant cache files safely. It must not bypass YouTube Music's access controls or claim offline playback where that is not supported.

## Acceptance tests

- A skipped track does not count as a completed play.
- Two qualifying completed plays of the same track within 7 days add it once.
- A third qualifying play does not create a duplicate playlist entry.
- Plays older than the rolling 7-day window do not count toward the threshold.
- Cache records older than 90 days are expired by the feature's own cleanup mechanism, without deleting unrelated files.
- App restart does not erase locally stored play timestamps.
- Unsupported cache or playlist hooks fail safely and are clearly documented.

## Status

Specification only. No patch implementation or APK has been built or tested yet.
