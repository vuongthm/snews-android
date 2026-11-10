# SNews — Security, Provenance and Release Notes

**Distribution name:** `snews-android` (renaming the outer repository directory does not change the Android package, Firebase app ID, source features or product name).

## Scope of this release

This edition adds the GitHub publication guide and aligns the folder hierarchy and bilingual report metadata with the proposed `snews-android` repository name. The app source and application ID have not been renamed for cosmetic reasons.


The user-provided `snews-app.zip` has been treated as the original Android source snapshot. This documentation package includes a sanitized **copy**, not a claim that the original repository history was changed. The Android application's general package structure, screens, ViewModels and repositories are retained; no standalone admin website or backend has been created or invented.

## Security-sensitive material detected

The original ZIP contained a literal VirusTotal API key in `app/src/main/java/com/example/securescan/viewmodel/ScanViewModel.kt` and a Firebase `app/google-services.json` bound to a particular Firebase project. `CloudinaryUploader.kt` included the Cloudinary cloud name and unsigned upload preset. The source key is potentially compromised if shared or committed previously. **Revoke/rotate the original VirusTotal key**, inspect existing Git history, and restrict related cloud services before publishing.

## Changes made to the shared copy

1. Removed `source/app/google-services.json`, machine-specific `.idea/` metadata, an unreferenced `data/models/data.json` sample containing phone-number records, and any local build directories from the packaged snapshot.
2. Replaced the literal VirusTotal key and Cloudinary identifiers with `BuildConfig` values read from ignored `source/local.properties`. The names are listed in `source/local.properties.example`.
3. Enabled `buildConfig = true` in `source/app/build.gradle.kts` and extended `source/.gitignore` for Google configuration, local settings and signing materials.
4. Added English documentation and a bilingual report set. Application feature logic has not been intentionally redesigned.

These adjustments improve repository hygiene **but do not secure API keys embedded in a compiled APK**. Production services that require secret credentials should be called through a trusted backend or provider-specific client-safe authentication model. Features relying on removed configuration will not work until legitimate local values are supplied.

## Code-level concerns requiring engineering review

**Scanner classification:** `ScanViewModel.kt` parses a formatted scan-response string to recover malicious counts and falls back to zero when parsing fails. Unknown, failed and clean states should not share an ambiguous classification.

**Authentication/UI:** the Google/Facebook/Apple callbacks wired in `MainActivity.kt` are empty. No claim of working social login is made.

**Bank-account lookup:** the account-number submit callback in `ScanPhoneAndCardScreen.kt` contains only a placeholder comment. Phone-number lookups are implemented separately using Firestore data, not universal fraud intelligence.

**Notifications:** `NotificationRepository.kt` reads records without explicit current-user filtering; the bulk “mark all as read” query targets all unread documents returned by Firestore. `NotificationSettingsViewModel.kt` contains TODO markers for persistence. Server-side Firestore rules and account-level test cases are required.

**Report/Cloudinary:** image evidence is sent to a third-party storage provider and may contain personal information. File scans are sent to VirusTotal; users should understand what data is transferred. Logs should not contain confidential URLs, files, personal records or API responses.

**Backend rules and authorization:** no Firebase Security Rules export or administrator backend is present in this ZIP. Access cannot be considered verified simply because Firebase Authentication is used.

## Validation performed / not performed

Performed: ZIP integrity/path validation, source tree inspection, direct verification of screen/viewmodel/repository/API references, release sanitization checks, DOCX render inspection and SHA-256 manifest generation. Not performed: Android Gradle Sync/debug build, execution on device/emulator, real Firebase access, live VirusTotal/Cloudinary calls, automated security scans, app signing, penetration testing or performance benchmarks.

## Safe Git publication checklist

Before your first push, check `git diff --cached`, ensure no historical secrets remain in Git history, remove any real `local.properties` and `google-services.json`, rotate previously exposed credentials, and confirm you have the rights to publish all images and example data. Keep original contributor credits and third-party licenses accurate. If a real key was ever committed to a remote repository, removing it from a later commit is not enough; it must be rotated.
