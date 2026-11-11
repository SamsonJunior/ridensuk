# RideNsuk – AI Okada & Keke Ride Hailing

Static web app (HTML/JS) + Firebase Auth + Firestore + Leaflet/OpenStreetMap + OSRM routing. No build step.

## 1. Firebase setup (once)
1. console.firebase.google.com > **Add project**.
2. **Build > Authentication > Get started > Email/Password > Enable**.
3. **Build > Firestore Database > Create database** (production mode).
4. Firestore > **Rules** tab > paste everything from `firestore.rules` > **Publish**.
5. **Project settings (gear) > Your apps > Web (</>)** > register app > copy the config into `firebase-config.js`.

## 2. Run in VS Code
Install the **Live Server** extension, right-click `index.html` > **Open with Live Server**.

## 3. Create the admin
1. Open the app and **Sign up** as a passenger with the email you want as admin.
2. Firebase Console > Firestore > `users` > that document > change `role` from `passenger` to `admin`.
3. Log out and log in. Admin can now **verify riders** (only verified riders get requests).

## 4. Host it (pick one)
- **Vercel**: put this folder on GitHub (upload files on github.com), then Vercel > Add New Project > import it > Deploy.
- **Firebase Hosting**: `npm i -g firebase-tools`, `firebase login`, `firebase init hosting` (public folder `.`), `firebase deploy`.
After deploying: Firebase > Authentication > Settings > **Authorized domains** > add your Vercel/Firebase domain. GPS needs HTTPS (hosting gives you this).

## How to test
Use two browsers (or one normal + one private window): one rider (verify in admin, go online, tap map to set location) and one passenger (tap pickup, tap drop-off, request).

## Notes
- Routes/distances come from the free public OSRM server (no live traffic data); fares use distance rules plus a peak-hour surcharge; matching ranks nearby verified riders by arrival time then rating. For heavy use, switch to a paid routing/maps provider.
- Not included (listed as future work in the report): payments, ratings, ML demand prediction.
