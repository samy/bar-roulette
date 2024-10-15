https://github.com/tttapa/docker-arm-cross-toolchain

sudo apt install cmake automake autoconf libtool intltool yasm libasound2-dev libpulse-dev libv4l-dev nasm git libglew-dev

git clone --branch release/5.2 https://gitlab.linphone.org/BC/public/linphone-sdk.git --recursive

cmake . -DLINPHONESDK_PLATFORM=Desktop  -DENABLE_OPENH264=ON  -DENABLE_LIME_X3DH=OFF -DENABLE_ADVANCED_IM=OFF -DENABLE_WEBRTC_AEC=OFF -DENABLE_UNIT_TESTS=OFF -DENABLE_MKV=OFF -DENABLE_FFMPEG=OFF -DENABLE_CXX_WRAPPER=OFF -DENABLE_NON_FREE_CODECS=ON -DENABLE_VCARD=OFF -DENABLE_BV16=OFF -DENABLE_V4L=ON -DENABLE_CONSOLE_UI=ON -DENABLE_DAEMON=ON -DENABLE_FLEXIAPI=OFF -DENABLE_QRCODE=OFF -DENABLE_VIDEO=OFF -DCMAKE_C_FLAGS="-O1" -DCMAKE_CXX_FLAGS="-O1" -DENABLE_SQLITE=OFF  -DENABLE_DB_STORAGE=OFF -DENABLE_ZRTP=OFF -DENABLE_VPX=ON --toolchain ~/opt/x-tools/armv8-rpi3-linux-gnueabihf/armv8-rpi3-linux-gnueabihf.toolchain.cmake
