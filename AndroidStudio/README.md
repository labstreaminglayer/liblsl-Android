# Introduction

Using Android Studio is presently the most robust and straightforward way to make Android apps that incorporate lab streaming layer. In this folder you will find build scripts and example applications.

The remainder of this document provides instructions on how to get started.

The scripts and documentation were tested most recently using Android Studio 4.0.1.

# Getting Started

## Requirements

You will need [liblsl-Java](https://github.com/labstreaminglayer/liblsl-Java). By default, the `settings.gradle` configuration file assumes the liblsl-Java folder will be found in `../../liblsl-Java`, but this can be overridden with `-Pliblsl_java_dir=path/to/liblsl-Java` or by modifying `settings.gradle`.

In turn, `liblsl-Java` will need to find the `liblsl` external build information. By default, liblsl-Java's `build.gradle` assumes it will find liblsl in `../liblsl` (relative to `liblsl-Java` folder).

> For local Java-only development, the liblsl-Java examples documentation instructs the user to download the compiled liblsl binary for their platform and put it in the same folder as liblsl-Java. However, in almost all Android development cases, liblsl will have to be compiled for the device target architecture and dropping in precompiled libraries is not appropriate.

For simplicity, you may want to clone the entire labstreaminglayer project tree, which includes liblsl-Android, liblsl-Java, and liblsl as submodules (as well as many more submodules you may never use): `git clone --recursive https://github.com/sccn/labstreaminglayer.git`.

`liblsl-Java` may require a recent [CMake](https://cmake.org/download/) version not yet included with Android Studio. See (`../../`)[`liblsl-Java/build.gradle`](https://github.com/labstreaminglayer/liblsl-Java/blob/master/build.gradle) to see the required CMake version and instructions on how to use a downloaded CMake over the bundled CMake.

## Build

### Provided Examples

Using Android Studio, open the `liblsl-Android/AndroidStudio` as the project folder.

If necessary, modify the created `local.properties` file to point to your newer CMake by adding the following line: `cmake.dir=C\:\\Program Files\\CMake`

In the dropdown box in the toolbar, select one of the modules (e.g. `SendStringMarkers`) then click on the green rightarrow run button.
As it is a dependency of the SendStringMarkers project, `liblsl.so` is built first for each target cpu architecture.

[liblsl-Java has more examples](https://github.com/labstreaminglayer/liblsl-Java/tree/master/src/examples) whose syntax should transfer to Android with almost no changes.

### Custom Applications

To make other LSL apps in Android Studio, the easiest way is to exit Android Studio, copy the SendStringMarkers folder and change every reference to SendStringMarkers in the copied folder to a new name (using a text editor).

If you would like to use LSL in an Android app built without Android Studio, it is recommended that you build one of the above Provided Examples in Android Studio then extract the needed compiled library files from the .apk file (using 7-zip or similar).

# Troubleshooting

jna is automatically downloaded and included. If something goes wrong verify your APK has `libjnidispatch.so` and `liblsl.so` in all CPU architecture dependent subdirectories of `lib`, e.g.

```
[your apk]
├── lib
│   ├── arm64-v8a
│   │   ├── libjnidispatch.so
│   │   └── liblsl.so
│   └── armeabi
│       ├── libjnidispatch.so
│       └── liblsl.so
...
```

# Known Issues

> labstreaminglayer\LSL\liblsl\CMakeLists.txt : C/C++ debug|x86 : CMake Deprecation Warning:
  The 'cmake-server(7)' is deprecated.  Please port clients to use the
  'cmake-file-api(7)' instead.
> Deprecated Gradle features were used in this build, making it incompatible with Gradle 7.0.
