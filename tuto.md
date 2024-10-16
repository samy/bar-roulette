docker build -t pi --build-arg DISK_SIZE=8G .
docker run --rm -p 2222:2222 -it -v $PWD/dist:/dist pi start


sudo apt install cmake automake autoconf libtool intltool yasm libasound2-dev libpulse-dev libv4l-dev nasm git libglew-dev ninja-build
//git clone --branch release/5.2 https://gitlab.linphone.org/BC/public/linphone-sdk.git --recursive
git clone --branch master https://gitlab.linphone.org/BC/public/linphone-sdk.git --recursive
git submodule update --init --recursive
cd linphone-sdk
mkdir build-raspberry
cd build-raspberry
cmake . -DLINPHONESDK_PLATFORM=Raspberry  -DENABLE_OPENH264=ON  -DENABLE_LIME_X3DH=OFF -DENABLE_ADVANCED_IM=OFF -DENABLE_WEBRTC_AEC=OFF -DENABLE_UNIT_TESTS=OFF -DENABLE_MKV=OFF -DENABLE_FFMPEG=OFF -DENABLE_CXX_WRAPPER=OFF -DENABLE_NON_FREE_CODECS=ON -DENABLE_VCARD=OFF -DENABLE_BV16=OFF -DENABLE_V4L=ON -DENABLE_CONSOLE_UI=ON -DENABLE_DAEMON=ON -DENABLE_FLEXIAPI=OFF -DENABLE_QRCODE=OFF -DENABLE_VIDEO=OFF -DCMAKE_C_FLAGS="-mfloat-abi=hard -mfpu=neon -march=armv8-a+simd+crypto+crc+sb -mtune=cortex-a53" -DCMAKE_CXX_FLAGS="-mfloat-abi=hard -mfpu=neon -march=armv8-a+simd+crypto+crc+sb -mtune=cortex-a53"  
make -j2 

