Track my bank! Android application
==================================

A mobile app to add transactions from your smartphone

How to use?
-----------

You must build your own apk, as you have to store some credentials within the app:
- the username
- the application key

Only your password will be prompted each time you open the app.

How to build?
-------------

This tutorial present how to build the app in a Linux system (with examples in Ubuntu).  
For other systems, please adapt it using external specific documentations.

### 1. Install [Android studio](https://developer.android.com/studio/), and launch it to configure it.  

### 2. Install cordova

```bash
sudo npm install -g cordova
```

### 3. Install SKDMAN!

```bash
curl -s "https://get.sdkman.io" | bash
```

### 4. Configure bash

Edit your `~/.bashrc` file and add this content:

```bash
export ANDROID_HOME=/home/$USER/Android/Sdk
export PATH=/home/$USER/Android/Sdk/tools:/home/$USER/Android/Sdk/tools/bin:/home/$USER/Android/Sdk/platform-tools:$PATH
```

(replacing $USER by your user).

Open a new bash

Run this command to accept all licenses:

```bash
sdkmanager --licenses
```

Answer "yes" to all prompts.

### 5. Install gradle

```bash
sdk install gradle 5.1
```

### 6. Clone this repository

git clone https://gite.flo-art.fr/floreal/trackmybank-app.git

### 7. Add credentials

Edit the file `www/js/credentials.js` and set here your application key (defined in the settings of your trackmybank webserver) and your username used to login.

### 8. Create keystore

```bash
keytool -genkey -v -keystore /path/to/android.keystore -alias trackmybank -keyalg RSA -keysize 2048 -validity 10000
```

(edit the path to the keystore in the command line)

### 9. Build APK

```bash
cordova build android --release -- --keystore="/path/to/android.keystore" --storePassword=<store_password> --alias=trackmybank --password=<key_password>
```

Now, install the generated apk in your smartphone!


Debugging
---------

You can run this app in an emulator on your computer (for debugging if you change the app).

1. You all previous step until step 7 included.
2. Open Android studio and create an empty project (we will not use it).  
3. Go to Tools -> AVD Manager, and create a new virtual device

### 4. Build the app

```bash
cordova build
```

### 5. Run the emulator

```bash
cordova run android
```

IOS
---

cordova is able to create ios apps too. I have not tested it. It's to your own risks.

Sources
-------

Pages I have read to build the initial app:

[https://www.pubnub.com/blog/how-to-convert-your-javascript-app-into-an-android-app-with-phonegap/](https://www.pubnub.com/blog/how-to-convert-your-javascript-app-into-an-android-app-with-phonegap/)

[https://cordova.apache.org/docs/en/8.x/guide/platforms/android/index.html](https://cordova.apache.org/docs/en/8.x/guide/platforms/android/index.html)
