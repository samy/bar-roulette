If you need to run the present project on anything than a Pi 2W, you may need to recompile.

As seen on https://wiki.linphone.org/xwiki/wiki/public/view/Linphone/Linphone%20and%20Raspberry%20Pi/:

# Install required dependencies
`sudo apt install cmake automake autoconf libtool intltool yasm libasound2-dev libpulse-dev libv4l-dev nasm git libglew-dev doxygen meson`  

Clone the linphone-sdk git repository on its latest stable branch (as of 2024/10/13 it is release/5.3).

`git clone --branch release/5.3 https://gitlab.linphone.org/BC/public/linphone-sdk.git --recursive`

# Compilation
Prepare compilation
```
cd linphone-sdk
cmake . -DLINPHONESDK_PLATFORM=Desktop -DENABLE_OPENH264=OFF  -DENABLE_LIME_X3DH=OFF -DENABLE_ADVANCED_IM=OFF -DENABLE_WEBRTC_AEC=OFF -DENABLE_UNIT_TESTS=OFF -DENABLE_MKV=OFF -DENABLE_FFMPEG=OFF -DENABLE_CXX_WRAPPER=OFF -DENABLE_NON_FREE_CODECS=ON -DENABLE_VCARD=OFF -DENABLE_BV16=OFF -DENABLE_V4L=OFF -DENABLE_CONSOLE_UI=ON -DENABLE_DAEMON=ON -DENABLE_FLEXIAPI=OFF -DENABLE_QRCODE=OFF -DENABLE_DOC=OFF -DENABLE_VPX=OFF -DENABLE_LDAP=OFF
```

Launch compilation (very long)

`make -j4`

Output binaries are on **linphone-sdk/desktop/bin** folder
