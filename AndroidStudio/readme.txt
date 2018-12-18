This is currently the most robust and straightforward way of making Android apps that incorporate LSL. These instructions apply to Android Studio 3.2.0. 

jna 4.5.0 is automatically downloaded and included, so just in case something goes wrong you'll have to make sure your APK has `libjnidispatch.so` and `liblsl.so` in all CPU architecture dependent subdirectories of `lib`, e.g.

[your apk]/lib
    arm64-v8a
        libjnidispatch.so
        liblsl.so
    armeabi
        libjnidispatch.so
        liblsl.so
...

To run, select the desired module from the list box the the left of the green arrow, and click the green arrow.

The majority of the native build instructions are in `../liblsl-Java/build.gradle` and `../liblsl/CMakeLists.txt`.

At this point, `liblsl.so` is built once for each target cpu architecture.

If you would like to use LSL in an android app built in a different way, it is recommended that you build one project (such as ReceiveStringMarkers) and extract the needed compiled library files from the .apk file (using 7-zip or similar).

To make other Apps in Android Studio, the easiest way is to exit Android Studio, copy the SendStringMarkers folder and change every reference to SendStringMarkers in the copied folder to a new name (using a text editor).

To see more examples of Java with LSL, look in LSL/liblsl-Java. Those examples should copy of to Android with minimal effort.
