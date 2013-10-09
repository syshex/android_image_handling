android_image_handling
======================

# NOT READY TO USE YET !!!!!!

This started out as a fork of : parallel-6/gradle_simple_crop_image_lib . This lib had a few problems, specially related to memory management when handling big images if a programmer didn't want to lose much resolution. This lead me to look for alternatives to handling images without running into OutOfMemory errors all the time. I came accross this post by [Android-Developer on StackOverflow](http://stackoverflow.com/questions/18250951/jni-bitmap-operations-for-helping-to-avoid-oom-when-using-large-images/) which has some really cool native c code that was easy to modify and use with simple_crop_image_lib, this StackOverflow post eventually turned into a lib aswell:  [AndroidJniBitmapOperations](https://github.com/AndroidDeveloperLB/AndroidJniBitmapOperations).

So in this lib we have a native implementation of a BitmapHolder that allows for the following operations done in Native:
- [x] Clock Wise Rotation
- [x] Counter Clock Wise Rotation
- [x] Cropping of Image

Regarding the CropImage Activities and stuff, it was modified to : 
- use a bit higher resolution images (2048 instead of 1024)
- use 1024 as fallback in case 2048 generates OOM
- use the native operation instead of the android SDK image manipulation, when possible

So, overall, this is not my original work, it is bits and pieces from other peoples work put together to make something a bit better. I improved stuff to fit my needs, and also implemented some more functionalities that i required.  So, credit where it is due:

## Original Work :

- https://github.com/AndroidDeveloperLB/AndroidJniBitmapOperations
- http://stackoverflow.com/questions/18250951/jni-bitmap-operations-for-helping-to-avoid-oom-when-using-large-images/
- https://github.com/sparallel-6/gradle_simple_crop_image_lib
- many many many other posts on StackOverflow and everywhere on the web.


# Compiling Native Bits

I've already provided a compiled native library in the repository, but if you would like to compile it yourself and make some changes then you'll need to download the [Android Native SDK](http://developer.android.com/tools/sdk/ndk/index.html). 
Once you have the NDK installed, just go into the  jni folder and run ndk-build. The output should look something like this:

```
rui@laptopjbay:~/projects/android_image_handling/jni$ /home/rui/Software/adt-bundle-linux-x86_64-20130219/android-ndk-r9/ndk-build 
Compile++ thumb  : JniBitmapOperations <= JniBitmapOperations.cpp
StaticLibrary  : libstdc++.a
SharedLibrary  : libJniBitmapOperations.so
Install        : libJniBitmapOperations.so => libs/armeabi/libJniBitmapOperations.so
rui@laptopjbay:~/projects/android_image_handling/jni$
```

that is it !
