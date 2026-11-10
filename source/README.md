# SNews — Android source code

SNews is an Android news-reading application with optional security-checking workflows. Originally developed in 2025 by **Trần Hoàng Minh Vương** and **Nguyễn Việt Tín**.

This release is distributed inside the `snews-android/` repository under `source/`. This release is based on the project's supplied source archive. The Kotlin/Compose application structure is preserved. For safer public distribution, the bundled snapshot omits the Firebase project configuration and replaces the hard-coded VirusTotal key and Cloudinary identifiers with local build-time configuration. These are **release-configuration changes**, not evidence of security validation.

To build, open `snews-android/source/` (this directory) in Android Studio, supply your own `app/google-services.json`, create `local.properties` with entries in `local.properties.example`, sync Gradle, then run the `:app` module on an Android device/emulator with API 24+. For exact steps and known limitations, read `../docs/SETUP_GUIDE.md`.

**Caution:** Build-time keys placed in an Android application can still be recovered from an APK. For production, protect privileged credentials behind a server-side service. Revoke/rotate the VirusTotal API key exposed in the original source snapshot before using the related service.

The supplied archive includes the mobile `:app` module only; a separate Flask administration server is **not** included.
