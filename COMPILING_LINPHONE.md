If you need to run the present project on anything than a Pi 2W, you may need to recompile.

The present steps may fail on your device (lack of RAM and CPU), you can compile it on a regular computer, using the [ptrsr/pi-ci](https://github.com/ptrsr/pi-ci) project. Please refer on the "Emulate Raspberry Pi for compiling" paragraph below.

Source: https://wiki.linphone.org/xwiki/wiki/public/view/Linphone/Linphone%20and%20Raspberry%20Pi/:

# Install required dependencies
`sudo apt install cmake automake autoconf libtool intltool yasm libasound2-dev libpulse-dev libv4l-dev nasm git libglew-dev ninja-build doxygen gcc-arm-linux-gnueabihf g++-arm-linux-gnueabihf g++ gcc -y`  

Clone the linphone-sdk git repository on master branch.

```
git clone --branch master https://gitlab.linphone.org/BC/public/linphone-sdk.git --recursive
cd linphone-sdk
git submodule update --init --recursive
```

# Compilation
Prepare compilation
```
cmake --preset=default -B build-desktop -DENABLE_LIME_X3DH=OFF -DENABLE_ADVANCED_IM=OFF -DENABLE_WEBRTC_AEC=OFF -DENABLE_UNIT_TESTS=OFF -DENABLE_MKV=OFF -DENABLE_FFMPEG=OFF -DENABLE_CXX_WRAPPER=OFF -DENABLE_NON_FREE_CODECS=ON -DENABLE_VCARD=OFF -DENABLE_BV16=OFF -DENABLE_V4L=ON -DENABLE_CONSOLE_UI=ON -DENABLE_DAEMON=ON -DENABLE_FLEXIAPI=OFF -DENABLE_QRCODE=OFF -DENABLE_VIDEO=OFF -DCMAKE_C_FLAGS="-march=armv8-a+simd+crypto+crc+sb -mtune=cortex-a53" -DCMAKE_CXX_FLAGS="-march=armv8-a+simd+crypto+crc+sb -mtune=cortex-a53" -DENABLE_OPENH264=OFF -DENABLE_PYTHON_WRAPPER=OFF -DENABLE_JAVA_WRAPPER=OFF -DENABLE_CSHARP_WRAPPER=OFF -DENABLE_CXX_WRAPPER=OFF -DENABLE_DOC=OFF -DENABLE_NON_FREE_FEATURES=ON -DENABLE_FIXED_POINT=ON -DENABLE_DB_STORAGE=OFF -DBUILD_SHARED_LIBS=OFF
```

Launch compilation (very long)

`make -j4`

Output binaries are on **linphone-sdk/desktop/bin** folder

# Emulate Raspberry Pi for compiling
My Pi Zero 2 was a little short for compiling, the process failed many times so I searched for a way to emulate the Pi on regular computers.
Emulate ARM CPUs is the most tricky part (x86 ISO of Raspbian can easyly run on Virtualbox).

You can use the [ptrsr/pi-ci](https://github.com/ptrsr/pi-ci) project which offers a Docker image emulating Pi operating system AND processor, using QEMU.

The default disk size of 2G of the Docker volume is too low for compiling, so you will need to increase it:

`docker run --rm -it -v $PWD/dist:/dist ptrsr/pi-ci resize 8G` (for 8Go volume)

You can run the Docker container with the following command (it will expose also a SSH on 2222 port):

`docker run -p 2222:2222 --rm -it -v $PWD/dist:/dist ptrsr/pi-ci start`
