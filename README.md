# WatchMoney

WatchMoney is an Android app built with Kotlin and Jetpack Compose. The current project already includes Firebase Auth, Firestore, test AdMob rewarded ads, points, history, manual withdrawal flow, notices, and withdrawal policy screens.

## Project Setup

- Language: Kotlin
- UI: Jetpack Compose
- Minimum Android SDK: 23
- Target Android SDK: 36
- Release version: `1.0.0` (`versionCode = 1`)

`app/google-services.json` must stay inside the `app/` module so Firebase Auth and Firestore can initialize correctly.

## Firestore Rules

This repository includes [firestore.rules](./firestore.rules), but these rules are not published automatically. They must be copied and published manually in the Firebase Console.

### How to publish Firestore rules

1. Open your Firebase project.
2. Go to **Firestore Database**.
3. Open the **Rules** tab.
4. Copy the full contents of `firestore.rules` from this repository.
5. Paste the contents into the Firebase Console editor.
6. Click **Publish**.

## Build Commands

Debug APK:

```bash
./gradlew clean assembleDebug
```

Release AAB:

```bash
./gradlew clean bundleRelease
```

Expected release bundle output:

```text
app/build/outputs/bundle/release/app-release.aab
```

## AdMob Notes

- The project is configured with AdMob test IDs only.
- Replace the test IDs with real production IDs only right before publication.
- Never click your own real ads after production rollout.

## Release Signing

Before uploading WatchMoney to the Play Store, configure a release signing key or Play App Signing upload key in Android Studio or your CI environment.

Do not commit signing secrets to GitHub. Keep the keystore file, `key.properties`, passwords, aliases, and upload key credentials outside the repository. This project ignores `key.properties`, `*.jks`, and `*.keystore` files to reduce the risk of accidentally publishing private signing material.

### Create a local upload keystore

Create the upload keystore on your own machine or secure CI environment. Do not create or store a real keystore in this repository.

Example command:

```bash
keytool -genkeypair -v -keystore upload-keystore.jks -keyalg RSA -keysize 2048 -validity 10000 -alias watchmoney
```

Keep `upload-keystore.jks` private. If this key is for Play App Signing, store it somewhere safe because it will be needed to upload future releases.

### Create local key.properties

Copy `key.properties.example` to a local file named `key.properties` in the project root and fill in your real local values:

```properties
storePassword=SUA_SENHA_DA_KEYSTORE
keyPassword=SUA_SENHA_DA_CHAVE
keyAlias=watchmoney
storeFile=upload-keystore.jks
```

Never send `upload-keystore.jks`, `key.properties`, passwords, aliases, or private signing material to GitHub. The repository keeps only `key.properties.example` as documentation.

### Generate a signed release AAB

After creating the local keystore and local `key.properties`, generate the signed release bundle with:

```bash
./gradlew clean bundleRelease
```

The expected output is:

```text
app/build/outputs/bundle/release/app-release.aab
```

## Checklist for Play Store

- Generate the release AAB.
- Create a privacy policy page.
- Fill in the Play Store Data Safety form.
- Fill in the content rating questionnaire.
- Create a short description.
- Create a full description.
- Prepare screenshots.
- Run a closed test if your Play Console account requires it.
- Replace AdMob test IDs with real ones only right before publication.
- Never click real ads from your own app.
