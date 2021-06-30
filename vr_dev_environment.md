# VR Development Environment

Tested on Windows 10 19042.1052 x86_64 & Unity 2020.3.12f1 & Oculus Quest 2 64GB

Inspired by: https://developer.oculus.com/documentation/unity/unity-tutorial

## Setup Unity For Android Development

- Link the Oculus device with your mobile phone via the Oculus application.
- Install Unity editor (Minimum supported version: 2019.4).
  - Additional required modules: Android Build Support (Android SDK & NDK tools, OpenJDK).
- Create a new Unity project via Unity Hub.
- Make sure Android Tools are mapped from: `Edit -> Preferences -> External Tools`.

## Configure Unity Project

- Under `Edit -> Build Settings`:
  - Set the platform to `Android` (In the next step, we'll configure the Oculus device).
  - Set the texture compression to `ASTC`.
  - Clear the `development build` section for the FINAL build as it may impact performance.
  - Save your settings with the `Switch platform` button.
- Under `Edit -> Project Settings -> Player`:
  - Fill the proper `Company Name`, `Product Name` and `Version`.
  - Down the same menu, under `Identification` section:
    - Make sure you set the correct `Version` and `Bundle Version Code`.
    - Set the minimum API level to `6.0 (Marshmallow)`, the target API should be `Automatic`.
  - Down the same menu, under `Configuration` section, make sure `Install Location` is `Automatic`.
- Under `Edit -> Project Settings`:
  - Select `XR Plugin Management` from the left menu pane, and click `Install XR Plugin Management`. Then, select the Android tab and mark the `Oculus` option - This enables VR support for Oculus.
- Under `Edit -> Project Settings -> Player`, Select the `Android` tab, and expand `Other Settings`, navigate to `Rednering` section.
  - Set `Color Space` to `Linear`.
  - Clear `Auto Graphics API`.
  - Make sure `OpenGLES3` is the first Graphics API.
  - Select `Multithreaded Rendering`.
- Under `Edit -> Project Settings -> Quality`:
  - Set `Pixel Light Count` to 1.
  - Set `Texture Quality` to `Full Res`.
  - Set `Anisotropic Textures` to `Per Texture`.
  - Set `Anti Alising` to `4x Multi Sampling`.
  - Clear `Soft Particles`.
  - Select `Realtime Reflections Probes`.
  - Select `Billboards Face Camera`.
- Under `Oculus -> Tools`: Click `Create store-compatible AndroidManifest.xml`.

## Setup Oculus Device For Development & Testing

### Setup Headset's Development Mode

- Turn on the headset.
- Navigate to `Settings -> More Settings -> Developer Mode`, and enable the feature.
- Connect the headset to your computer with USB Type-C cable.
- Inside the headset's interface, confirm USB debugging.

### Development & Testing

- Inside your Unity project, navigate to `File -> Build Settings`.
- Make sure the platform is set to Android.
- Choose your headset from the `Run Device` drop-menu.

### Advanced: Enable Bridge Debugging

- Make sure the headset is connected to the computer.
- For windows only, download the [OEM drivers](https://developer.oculus.com/downloads/package/oculus-adb-drivers/).
- Open a terminal, and run: `adb devices` (ADB should be installed with Android's SDK).

### Installing APKs with ADB

- After building our application, Unity should output an APK file.
- In a terminal, run: `adb install -r [APK_PATH]`
- Find your installed app in: `Library -> Unknown Sources` .