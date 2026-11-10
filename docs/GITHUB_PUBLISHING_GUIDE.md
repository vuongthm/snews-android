# SNews Android — GitHub Publishing Guide

## Repository identity

The product is called **SNews**. The recommended GitHub repository name is **`snews-android`**, and its planned account path is `vuongthm/snews-android`. Original development took place in **2025**; the first publication commit should keep its actual date (for example, a 2026 publication). Both original contributors remain credited in `CREDITS.md`.

The outer directory, `snews-android/`, is the repository root. The Android Studio project lives inside `source/`. This deliberate separation keeps project reports and end-user documentation out of the Gradle build root. In `source/settings.gradle.kts`, the original Gradle project name remains `SNews`. The Android `applicationId` and Kotlin namespace remain `com.example.securescan`; changing them is a separate Android/Firebase migration, **not** part of this repository rename.

## Create the remote repository

Sign in to GitHub and create a repository named `snews-android` under your own account. For an existing working copy, confirm that the local `snews-android/` folder contains this README, `report/`, `docs/` and `source/`. Do not accidentally publish the parent directory containing other files. Choose the repository visibility and licensing deliberately. If you plan to push a first commit from this package, create the GitHub repository **without** auto-generating a separate README or .gitignore to avoid a needless initial merge.

## Verify before staging

Review `docs/SECURITY_AND_RELEASE_NOTES.md` before publishing. In particular, the original source archive exposed a VirusTotal key: **rotate/revoke it** even though this sanitized package omits the literal value. Never commit actual `source/local.properties`, `source/app/google-services.json`, Firebase service-account credentials, keystores, personal report evidence or private example phone-number records. Inspect the entire staged diff and Git history if reusing the former repository. The build may require locally supplied Firebase configuration but those files must stay untracked.

Run these commands from **inside `snews-android/`**:

```bash
git init
git branch -M main
git add .
git status
git diff --cached --stat
git diff --cached --check
```

Review all staged paths and confirm there are no credentials. If the new repository is empty and you approve the changes, make the initial commit and push:

```bash
git commit -m "feat: publish SNews Android project (2025) with bilingual reports"
git remote add origin https://github.com/vuongthm/snews-android.git
git push -u origin main
```

If a remote named `origin` already exists, inspect it with `git remote -v` and update it intentionally rather than blindly running `remote add`. If you **rename** the original GitHub repository instead of creating a new one, preserve history by renaming the existing repository through GitHub settings and update your local `origin` URL. GitHub may redirect the old link, but revise README links to the canonical new location after publication.

## Suggested GitHub metadata

**Description:** SNews is an Android news reader with integrated URL, file and phone-number safety checks, built with Kotlin, Jetpack Compose and Firebase.

**Topics:** `android`, `kotlin`, `jetpack-compose`, `firebase`, `android-app`, `news-reader`, `cybersecurity`, `mvvm`, `virustotal`

The VirusTotal-powered result is advisory and not a guarantee of safety. Do not describe the project as a certified malware scanner or a fully tested security product.

## Review after publishing

Open the repository page and confirm that `README.md` renders at the root; `source/settings.gradle.kts` exists; both `.docx` files open in `report/`; and English guides are linked correctly. Follow `docs/SETUP_GUIDE.md` to configure a **fresh local** Firebase project and test the app. The documentation package was statically reviewed, not tested on a running Android device. Do not represent Gradle build, Firebase authorization, scanner accuracy or a live release as verified until you run those checks yourself.

A license is not bundled. If you want other people to reuse the original code, select an explicit license you are authorized to grant while retaining attribution to original contributors and third-party components.
