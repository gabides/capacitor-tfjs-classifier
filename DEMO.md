# Capacitor-tfjs-classifier - Full Demo steps

## Step 0 - prepare setup
```bash
yarn add @ionic/cli@latest
yarn ionic config set -g npmClient yarn
```
### create repo from template
```bash
yarn ionic start capacitor-tfjs-classifier tabs --name capacitor-tfjs-classifier --type vue
cd ./capacitor-tfjs-classifier
```

### add native platforms
```bash
yarn ionic capacitor add ios
yarn ionic capacitor add android
```

### build
```bash
yarn build
yarn sync
yarn cap open ios
yarn cap run ios
```

##  Step 1 - Add custom code for app design/content (without camera/tfjs)
- `demo-code/step1-design-navigation/TabsPage.vue`
- `demo-code/step1-design-navigation/Tab1Page.vue`


##  Step 2 - add camera preview code
### add camera-preview plugin
```bash
yarn add @capacitor-community/camera-preview@2.1.0 
```

### add camera authorization to Android and iOS:

#### Android
In `android/app/src/main/AndroidManifest.xml` above the closing `</manifest>` tag add this line to request the CAMERA permission:
```xml
<uses-permission android:name="android.permission.CAMERA" />
```

## iOS
In `ios/App/App/Info.plist` add permissions with the raw keys `NSCameraUsageDescription` and `NSMicrophoneUsageDescription`.

```plist
<key>NSCameraUsageDescription</key>
<string>App needs camera permission to classify object in the camera feed</string>
<key>NSMicrophoneUsageDescription</key>
<string>App needs microphone permission</string>
```

### add code for camera preview
- `demo-code/step2-camera-preview/Tab1Page.vue`


##  Step 3 - add tensorflow and inference code
### add tensorflowfjs package
```bash
yarn add @tensorflow/tfjs
```

### add code for inference
- `demo-code/step3-image-classification/Tab1Page.vue`
- `demo-code/step3-image-classification/services/image-classification.service.ts`
- `demo-code/step3-image-classification/services/classes.ts`
