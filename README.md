[![Build Status](https://travis-ci.org/kiwix/kiwix-android.svg?branch=master)](https://travis-ci.org/kiwix/kiwix-android)

Kiwix is an offline reader for Web content. It's especially thought to
make Wikipedia available offline.  This is done by reading the content
of the project stored in a file format ZIM, a high compressed open
format with additional meta-data.

Android is just an additional target but you can still build for
Android only from a Linux or Mac (it cross-compiles).

* ./autogen.sh

* ./configure --disable-staticbins --disable-manager --disable-server --disable-launcher --disable-indexer --disable-installer --disable-searcher --disable-reader --disable-components --enable-android --enable-compileall

* cd src/dependencies && make android-deps && cd -

* cd android && ./build-android-with-native.py (If you have problem with aapt on a 64bits Linux, you might have to install 32 libsm on Ubuntu: lib32gcc1, lib32stdc++6, lib32z1)

To install the newly created APK on your device, use the following script:
./android/install-kiwix-on-device.sh

# CUSTOM APPS 

Android Custom App are single-content Kiwix-android clones. Those app
are tied to a single content and CAN NOT open other zim file. As well,
bundled zim files are not readable by the regular Kiwix app. Custom
App have specific branding.

Custom App are either compiled as embed (ZIM file is included in APK)
or are accompanied by a ZIM file.

* Embedded versions can be very large (while Play Store have a 50MB
  limit)
* Non-embedded versions are small (6MB) but require a companion ZIM file
  which can be up to 2GB.
* Companion file is a feature of the Play store.

Steps to build a Custom App:

0. Install following requirements

1. Build your first APK

* Generate your icon using `gen-std-icon.py logo-file.png lang_code`
* For creating a corresponding custom app icon of our widget, please follow these subinstructions:
  a) Go to this icon generator -> https://goo.gl/6QtNGJ
  b) Click select image and upload your custom app icon .png
  c) Download zip, extract, select all drawable folder (hdpi,mdpi...)
  d) Paste in project's drawable folder (replace existing icon)
* Prepare your JSON file using the sample in the script
* Choose your package name wisely.
** org.kiwix.kiwixcustomXXXXXX
** o not add levels. Do not use dash or underscores !
** Use version_code: 1 at first
* Build your APK with `gen-custom-android-build.py my-file.json`

2. Go to the Developer Page on https://play.google.com/apps/publish
and create a new Application and give it a name.

3. Fill the Store listing section with decent information
* App Title (30 chars)
* App Short Description (80 chars)
* App Description (4,000 chars)

* Add 2 screenshots
* Add the 512px icon
* Add feature graphic (1024x500)

* Select Application Type (Applications)
* Select Category (Education|Books & Reference|Health & Fitness|...)
* Select Content Rating (High Maturity|Medium Maturity|Low
  Maturity|Everyone)
* Add an email Address
* Check the "Not submitting a privacy policy URL" box

4. Go to Content Rating Tab
* Fill the Questionnaire
** Email address
** Select category
** Check "No" for each question
* Hit Calculate rating
* Hit Apply rating

5. Go to Pricing & Distribution
* Check "SELECT ALL COUNTRIES" box
* Check "Content guidelines"
* Check "US Export laws"

6. Go to APK 
* Go to Alpha Testing
* Manage list of testers (Add
  https://plus.google.com/communities/106410746144853739922)
* Upload an APK (Use a proper APK (version 1 usually) with correct
  package name)

7. Build a second APK
* Change version_code in JSON file
* Rebuild

8. Upload your second APK using the upload script:
$GOOGLE_API_KEY=/home/xxx/google-api.p12
$python3 ./upload-apk.py my-file.json`

9. [whenever you feel the need to] Update Play Store listing using
play-store script.

To update the apk only without a content update:

# CUSTOM APPS - APK UPDATE ONLY

1. Add the "content_version_code" field to json file and set it to the
version code of the expansion file you want (check google play to find
this).  Increment the actual version code.

2. Ensure the content file is located locally. Without this the
app will think that it is corrupt.

3. Compile as usual.

4. Sign and upload to the Google Play store.

5. When uploading you are given the choice of which expansion file to
use.  Make sure to tell Google the right one.

6. Publish

# APK WITH ZIM FILE 

To make an APK which embeds a ZIM file:
* In the json file, add:
    "embed_zim": true,
* You might need to set up following env. variable:
    _JAVA_OPTIONS="\"-Xmx4096m\" \"-Xms4096m\""

# CONTACT 

Email: kiwix-developer@lists.sourceforge.net or contact@kiwix.org
Jabber: kelson@kiwix.org
IRC: #kiwix on irc.freenode.net

You can use IRC web interface on http://chat.kiwix.org/

More... http://wiki.kiwix.org/wiki/Communication


# LEGAL & DISCLAIMER 

Read '../COPYING' file
