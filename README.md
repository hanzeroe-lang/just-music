# Just music

Just music is a free, open-source music player for Android. It opens straight into the app, has no subscription screen, and every feature that the build supports is enabled for every user.

This repository is a **standalone project**, not a GitHub fork. It was created from the source of [Orb Music v1.8.5.Radiant](https://github.com/theusalbuquerque/orb/releases/tag/v1.8.5.Radiant), which is published under the GNU General Public License v3.0. The original license and notices are preserved in [LICENSE](LICENSE), and the changes made here are described below.

## What is different from the upstream release

- **New app identity** — named *Just music*, with application ID `com.music.justmusic` and its own release signing key. It installs alongside Orb and does not receive Orb updates.
- **New launcher icon** — a black glyph on a white background, supplied as an Android vector drawable and adaptive icon. Source SVG: [`docs/just-music-icon.svg`](docs/just-music-icon.svg).
- **No launch animation** — the animated splash composable was removed and cold starts go directly to the main screen.
- **No premium subscription** — all locally gated features (Automix 2.5, maximum-quality downloads, offline lyrics, Orb Switch and related switches) are enabled unconditionally, and the subscription card/paywall rows are hidden.
- **Standalone release channel** — in-app update checks point to this repository instead of the upstream one.

Some features still talk to third-party or upstream online services (for example account sync, community statistics, or server-backed analysis). Those services are outside this repository and may require credentials of their own. Removing the local paywall does not change how those external services behave.

## Building

Use Android Studio (or the command line with the Android SDK installed). The project targets SDK 36, uses NDK 28.2.13676358 and CMake 3.22.1, and needs **JDK 21** for the Kotlin Gradle plugin.

```powershell
# local.properties (not committed)
sdk.dir=C\:\\Users\\<you>\\AppData\\Local\\Android\\Sdk

# keystore.properties (not committed) — use your own key for your own releases
storeFile=justmusic-release.jks
storePassword=...
keyAlias=justmusic
keyPassword=...

.\gradlew.bat :app:assembleProdRelease
```

The signed APK is written to `app/build/outputs/apk/prod/release/JustMusic-<version>.apk`.

If you publish your own build, generate your own signing key (`keytool -genkeypair ...`) and keep it private. The key used for the published release in this repository is intentionally not committed.

## License

Just music is distributed under the **GNU General Public License v3.0** ([LICENSE](LICENSE)), the same license as the upstream source. It is free software: you can redistribute it and/or modify it under the terms of the GPL.

Upstream attribution: source derived from [theusalbuquerque/orb](https://github.com/theusalbuquerque/orb) at tag `v1.8.5.Radiant`; original work © the upstream authors. This is a modified version; all changes listed above are © this repository's contributors.
