# Threadly

| Folder | What | Deploy |
|---|---|---|
| apps/storefront-web | Editorial storefront website (single file) | Any static host / WordPress / Vercel |
| apps/admin-web | Admin panel: products, payments, shipments | Static host behind login |
| apps/storefront-mobile | Glass-style storefront, wrapped as Android app | APK |
| apps/admin-mobile | Admin panel, wrapped as Android app | APK |

## Get the APKs (no Android Studio needed)
1. Create a GitHub repo and push this folder.
2. Open the Actions tab and wait for "Build APKs" to finish (about 5 minutes).
3. Download `storefront-mobile-apk` and `admin-mobile-apk` from the run's Artifacts.
4. Unzip and install `app-debug.apk` on the phone (allow install from unknown sources).

## Build locally instead
Needs Node 20, JDK 17 and Android Studio (for the SDK).
```
cd apps/storefront-mobile
npm install
npx cap add android
npx cap sync android
cd android && ./gradlew assembleDebug
```
APK: `android/app/build/outputs/apk/debug/app-debug.apk`

## Notes
- Debug APKs are for testing. For Play Store you need a signed release AAB (`./gradlew bundleRelease` plus a keystore).
- All data is sample data in each file. Next step is replacing the sample arrays with Shopify Storefront API (store) and Shopify Admin API + Razorpay (admin).
- Admin has no login yet. Do not host it publicly before adding auth.
