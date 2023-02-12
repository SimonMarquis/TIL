---
title: 🔥 Firebase
---

### Firebase local hosting

???+ quote
	Firebase Hosting reserves URLs in your site beginning with `/__`. This reserved namespace makes it easier to use other Firebase products together with Firebase Hosting.  
	These reserved URLs are available both when you deploy to Firebase (`firebase deploy`) or when you run your app on a local server (`firebase serve`).

```html
<!-- Insert these scripts at the bottom of the HTML, but before you use any Firebase services -->
<!-- Firebase App (the core Firebase SDK) is always required and must be listed first -->
<script src="/__/firebase/x.y.z/firebase-app.js"></script>

<!-- Add Firebase products that you want to use -->
<script src="/__/firebase/x.y.z/firebase-auth.js"></script>
<script src="/__/firebase/x.y.z/firebase-firestore.js"></script>

<!-- Load the Firebase SDKs before loading this file -->
<script src="/__/firebase/init.js"></script>
```

[🔗](https://firebase.google.com/docs/hosting/reserved-urls) [🔗](https://firebase.blog/posts/2017/04/easier-configuration-for-firebase-on-web)

### Backup & Restore

- :material-cloud-download-outline: Backup
    ```bash
    gsutil -m cp -R gs://xyz.appspot.com .
    firebase database:get / --pretty > xyz.json
    ```
- :material-cloud-upload-outline: Restore
    ```bash
    gsutil -m cp -R . gs://xyz.appspot.com
    firebase database:set / xyz.json
    ```
