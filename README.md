# SNews

**Repository:** `snews-android`  ·  **Product:** SNews  ·  **Platform:** Android  ·  **Original development:** 2025

**An Android news reader with contextual safety-checking workflows.**

SNews was developed as a 2025 software project by **Trần Hoàng Minh Vương** and **Nguyễn Việt Tín**. The application brings news reading, article interaction, saved posts, user reports, and optional URL/file/phone checks into a single Android experience. This repository package provides the Android source and bilingual product reports.

## Project overview

The Android client is written in Kotlin and Jetpack Compose. Navigation and ViewModels connect screens to repositories using Firebase Authentication and Cloud Firestore. Additional integrations cover VirusTotal URL/file analysis, Cloudinary image uploads, an external cybersecurity RSS feed, and ML Kit article translation. The code is a **single `:app` Gradle module**, not a supplied backend or administration dashboard.

The project is best presented as a **documented source release**, not a certified security product. Runtime scanning depends on external service configuration. A threat-intelligence service returning no detections does not guarantee that a link, file, or phone number is safe.

## Repository layout

```text
snews-android/
├── report/
│   ├── SNews_Project_Report_EN.docx
│   ├── SNews_Project_Report_VI.docx
│   └── README.md
├── docs/
│   ├── SETUP_GUIDE.md
│   ├── USER_GUIDE.md
│   ├── SOURCE_CODE_GUIDE.md
│   ├── ARCHITECTURE_GUIDE.md
│   ├── SECURITY_AND_RELEASE_NOTES.md
│   ├── VERIFICATION_MATRIX.md
│   ├── FILE_MANIFEST.sha256
│   └── GITHUB_PUBLISHING_GUIDE.md
├── source/                 # Android Studio / Gradle project
├── CREDITS.md
└── README.md
```

## Getting started

**Start in `snews-android/`** (the documentation repository root), then open **`source/`** as the Android Studio/Gradle project. These two directories serve different purposes.


Open **`source/`** in Android Studio. The included project uses Android Gradle Plugin 8.8.1, Kotlin 2.0.0, `compileSdk 35`, `minSdk 24`, and Java 11 source compatibility; run Gradle with a compatible JDK (typically JDK 17 for this AGP version). Provide your **own** Firebase configuration and local service configuration before building. Follow [the setup guide](docs/SETUP_GUIDE.md) rather than copying any credentials from an earlier commit or the original archive.

## GitHub publication

This release is prepared for a repository named **`snews-android`**. The published destination is intended to be `vuongthm/snews-android`; it does **not** imply that a remote repository has already been created or pushed. See the [GitHub publishing guide](docs/GITHUB_PUBLISHING_GUIDE.md) for first-push instructions and a checklist for avoiding accidentally publishing credentials.

## Feature status

News navigation, article detail, search, comments/reactions, bookmarks, reports, RSS, translation, Firebase email/password account logic and URL/file scanning have identifiable screen and repository implementations. Phone lookups query Firestore collections. Bank-account scanning is a placeholder; social sign-in handlers are not connected. Notification preferences are not persisted, and Firebase Security Rules were not provided. See [Verification Matrix](docs/VERIFICATION_MATRIX.md) for the exact scope and code references.

## Release safety and provenance

This public-share snapshot is derived from the project source archive supplied by its owner and is packaged under the new repository directory name `snews-android/`. It excludes the original `app/google-services.json`, `.idea` metadata, local settings and possible signing material; it replaces hard-coded VirusTotal and Cloudinary configuration values with locally supplied build settings. **These changes do not make a mobile API key secret once packaged into an APK.** Rotate the original exposed VirusTotal key and use an authenticated backend for privileged production traffic. Details are recorded in [Security & Release Notes](docs/SECURITY_AND_RELEASE_NOTES.md).

No build, end-to-end test, service permission review or malware-detection benchmark was completed in the documentation environment. Both Word reports describe the project as a product and technical system, and are not certificates of operational security.

## Credits

Original project authors: **Trần Hoàng Minh Vương** and **Nguyễn Việt Tín** (2025). Third-party frameworks, APIs and design resources retain their own authorship and licenses. See [CREDITS.md](CREDITS.md).
