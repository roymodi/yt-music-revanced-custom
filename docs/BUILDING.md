# Development and build setup (Windows)

This is a starting guide. The exact Gradle tasks and CLI arguments depend on the current ReVanced patcher/CLI versions and the build files added to this repository.

## 1. Install tools

Install:

- [Git for Windows](https://git-scm.com/download/win)
- [Java JDK](https://adoptium.net/temurin/releases/) matching the current upstream project's requirements
- [Visual Studio Code](https://code.visualstudio.com/)
- [Android SDK Platform Tools](https://developer.android.com/tools/releases/platform-tools) if you want to use ADB

Open PowerShell and verify:

```powershell
git --version
java --version
javac --version
```

Do not assume a particular Java version until you check the current upstream Gradle configuration and setup instructions.

## 2. Clone this repository

```powershell
mkdir D:\vscode\Android -Force
Set-Location D:\vscode\Android
git clone https://github.com/roymodi/yt-music-revanced-custom.git
Set-Location .\yt-music-revanced-custom
code .
```

## 3. Review upstream requirements

Read the current [ReVanced development setup](https://github.com/ReVanced/revanced-documentation/blob/main/docs/revanced-development/1_setup.md) and the [CLI usage guide](https://github.com/ReVanced/revanced-cli/blob/main/docs/1_usage.md). Confirm the current patcher API, build toolchain, and supported YouTube Music app version before writing patches.

The upstream ReVanced Patches source has been hosted at [the ReVanced Patches project](https://gitlab.com/ReVanced/revanced-patches/); check the official project for the current canonical location.

## 4. Build status

The repository is currently a documentation scaffold and does not yet contain a Gradle project or custom patch bundle. Therefore, `gradlew.bat build` and APK patching commands are **not available yet**.

The next development step is to add a minimal patch module using the current upstream APIs, then verify that it builds before implementing features.

## 5. APK patching and testing

Once a compatible patch bundle and CLI have been built/downloaded from trusted official releases:

1. Read the CLI's own help output to confirm arguments for that exact version.
2. Use a base APK version supported by the selected patches.
3. Keep a backup of important app data before replacing an installed app.
4. Install the resulting APK on a test device and verify the behavior.
5. Record the exact base app version, patch version, CLI version, and test results.

A patched APK usually has a different signing certificate from the Play Store app and may not install as an in-place update. Do not uninstall the original until you understand the data-loss implications.

## Security and distribution

- Never publish signing keys, passwords, tokens, or private credentials.
- Do not commit proprietary APKs or generated binaries to this source repository.
- Use GitHub Releases or build artifacts for appropriate project outputs, after reviewing applicable licensing and redistribution terms.
