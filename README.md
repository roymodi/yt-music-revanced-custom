# YouTube Music ReVanced Custom

A community project for developing and testing custom patches and configuration around **ReVanced-compatible YouTube Music builds**.

> **Status: Initial scaffold.** This repository does not yet contain a working custom patch bundle or a built APK. Features listed in the roadmap are goals, not implemented features.

## Goals

- Develop small, reviewable custom patches compatible with the relevant ReVanced patcher APIs.
- Explore playback, appearance, audio controls, and settings improvements where technically feasible.
- Document repeatable builds on Windows with PowerShell and VS Code.
- Keep source code and build instructions in Git; distribute build artifacts separately when appropriate.

## Important notes

- YouTube Music is proprietary software. This project does **not** include Google's source code or an official YouTube Music APK.
- Obtain any base APK yourself from a legitimate source and ensure it matches the patch set's supported package/version.
- Patch compatibility changes over time. Always check the current upstream ReVanced documentation and patch compatibility before building.
- Do not commit APKs, signing keys, passwords, access tokens, or other secrets.
- Keep upstream notices, attribution, and license requirements intact. Review the applicable licenses before redistributing modified code or builds.
- This is an independent community project and is not affiliated with or endorsed by Google or the ReVanced team.

## Repository layout

```text
yt-music-revanced-custom/
├── README.md
├── .gitignore
├── docs/
│   ├── BUILDING.md
│   └── REPEATED_SONG_CACHE_FEATURE.md
└── patches/
    └── README.md
```

## Getting started

See [docs/BUILDING.md](docs/BUILDING.md) for Windows, Java, Gradle, and ReVanced development setup notes.

## Roadmap

- [ ] Confirm the current upstream patching API and supported YouTube Music version.
- [ ] Add a minimal custom patch module that builds successfully.
- [ ] Add automated build/test checks after the project build system is selected.
- [ ] Implement the cache-age and repeated-playlist feature described in [docs/REPEATED_SONG_CACHE_FEATURE.md](docs/REPEATED_SONG_CACHE_FEATURE.md), starting with reliable local play tracking.
- [ ] Add audio/playback improvements only after compatibility and behavior can be verified.
- [ ] Document install, rollback, and troubleshooting steps.

## Upstream references

- [ReVanced Patches](https://gitlab.com/ReVanced/revanced-patches/)
- [ReVanced CLI](https://github.com/ReVanced/revanced-cli)
- [ReVanced development setup](https://github.com/ReVanced/revanced-documentation/blob/main/docs/revanced-development/1_setup.md)
- [ReVanced CLI usage](https://github.com/ReVanced/revanced-cli/blob/main/docs/1_usage.md)

## Contributing

Please open an issue describing the intended change and target app version before making a large patch. Keep changes focused and include build/test evidence where possible.
