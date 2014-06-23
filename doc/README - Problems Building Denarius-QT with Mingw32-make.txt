This one wasn't straightforward nor obvious how to get it built without quite a bit of wasted time and headache. To save you the trouble this version has a few slight changes made to it to get it running.

First off, the biggest change was made to util.h and util.cpp
Please see https://github.com/laanwj/bitcoin/commit/61d85071405b99c3734606eed31ea8f615c0c77a#diff-772f489c7d0a32de3badbfbcb5fd200dR538

These changes are necessary because of some problem with mingw that I didn't take the time to understand. You'll need to check if the repo you're trying to build from has this change made.

In the denarius-qt.pro I changed a few things. In order to build a static executable, ensure the boost suffix is -mgw48-mt-s-1_55 (version numbers may differ, but the -mt-s- is important to target the right libs.

Also the following needs to be added:

Line 7: CONFIG += static

The following needs to be added to the deps (make sure you set proper directory name):

QRENCODE_INCLUDE_PATH=C:/deps/qrencode-3.4.3
QRENCODE_LIB_PATH=C:/deps/qrencode-3.4.3/.libs

And the following needs to be added directly under the macx:QMAKE_LFLAGS:

win32:QMAKE_LFLAGS *= -Wl,--large-address-aware -static

When you run qmake, make sure you use "RELEASE=1" "USE_IPV6=1" "USE_QRCODE=1" as arguments. UPNP is not used.

Then run: mingw32-make -f -Wno-unused-variables Makefile.Release

I used QT Creator with QT 4.8.5 to do the build but it'll work from the cli too. 

Compliments of Edric.