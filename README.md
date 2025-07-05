# Android NDK GIF Library (16KB Aligned)

GIF library built with NDK and Gradle in AAR format for usage with Android Gradle build system.

## 🚀 v1.0.2 - Google Play Store Ready!

This version includes **16KB page alignment** to meet Google Play Store requirements for devices with 16KB memory pages.

### ✅ What's New in v1.0.2
- **16KB memory alignment** for Google Play Store compliance
- **CMake build system** migration from ndk-build
- **All architectures supported** (arm64-v8a, x86_64, armeabi-v7a, x86)
- **Verified compatibility** with Google's alignment verification tool
- Ready for immediate Google Play Store submission

### 📋 Previous Changes (v1.0.1)
- Added GIF Image Iterator for Image decoding
- Fixed a problem of residual image on transparent background

## 🎯 Google Play Store Compatibility

This library is now fully compliant with Google Play Store's 16KB alignment requirements:

```
lib/armeabi-v7a/libandroidndkgif.so: ALIGNED (2**14) ✅
lib/x86/libandroidndkgif.so: ALIGNED (2**14) ✅  
lib/arm64-v8a/libandroidndkgif.so: ALIGNED (2**14) ✅
lib/x86_64/libandroidndkgif.so: ALIGNED (2**14) ✅
```

## 📦 Installation

### JitPack (Recommended)
```groovy
repositories {
    maven { url 'https://jitpack.io' }
}

dependencies {
    implementation 'com.github.DonMarv00:android-ndk-gif-16kb:v1.0.2'
}
```

### Maven Central (Original)
```groovy
repositories {
    maven { url 'https://repo1.maven.org/maven2' }
}

dependencies {
    implementation 'io.github.waynejo:androidndkgif:1.0.1'
}
```

## 🎨 Encoding Options

- **ENCODING_TYPE_SIMPLE_FAST** - Low memory, fast encoding, lower quality
- **ENCODING_TYPE_FAST** - Fast encoding with better quality  
- **ENCODING_TYPE_NORMAL_LOW_MEMORY** - Lower memory usage, dynamic image changing
- **ENCODING_TYPE_STABLE_HIGH_MEMORY** - Highest quality, stable sequence, more memory

## 💻 Usage

### Decoding with Iterator (Memory Efficient)
```java
GifDecoder gifDecoder = new GifDecoder();
final GifImageIterator iterator = gifDecoder.loadUsingIterator(destFile);
while (iterator.hasNext()) {
    GifImage next = iterator.next();
    if (null != next) {
        imageView.setImageBitmap(next.bitmap);
    }
}
iterator.close();
```

### Standard Decoding
```java
GifDecoder gifDecoder = new GifDecoder();
boolean isSucceeded = gifDecoder.load(destFile);
if (isSucceeded) {
    for (int i = 0; i < gifDecoder.frameNum(); ++i) {
        Bitmap bitmap = gifDecoder.frame(i);
    }
}
```

### Encoding
```java
GifEncoder gifEncoder = new GifEncoder();
gifEncoder.init(width, height, filePath, GifEncoder.EncodingType.ENCODING_TYPE_NORMAL_LOW_MEMORY);
// Bitmap MUST be ARGB_8888
gifEncoder.encodeFrame(bitmap1, delayMs);
gifEncoder.encodeFrame(bitmap2, delayMs);
gifEncoder.close();
```

## 🔧 Build Requirements

- **CMake:** 3.22.1+
- **NDK:** 25.0+ (tested with 29.0.13599879)
- **Gradle:** 8.11.1+
- **Java:** 17+

## 📝 Reference

GIF Decoder is originally based on [android-gifview](https://code.google.com/p/android-gifview/).

---
![Google Play Store Ready](https://img.shields.io/badge/Google%20Play%20Store-16KB%20Aligned-brightgreen)
