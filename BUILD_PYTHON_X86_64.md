## Python for Android *steps for building on X86_64*
For other archs, please review according file:
* BUILD_PYTHON_ARM.md
* BUILD_PYTHON_X86_64.md or 
* BUILD_PYTHON_X86.md

Python can be built for android using the termux python package.

Prerequisites : git, docker

    git clone https://github.com/termux/termux-packages
    cd termux-packages

create a file `build-python.sh` with below content

    #!/bin/bash
    export TERMUX_ARCH=x86_64
    export TERMUX_PREFIX=/data/youtubedl-android/usr
    export TERMUX_ANDROID_HOME=/data/youtubedl-android/home
    ./build-package.sh python

Make file executable

    chmod +x ./build-python.sh
    
Build Package

    ./scripts/run-docker.sh ./build-python.sh
    
This will create several `.deb` files in `debs/` directory.  
I have found the following packages to be sufficient for youtube-dl to work.

    python_3.7*.deb
    libandroid-support_24*.deb
    libutil*.deb
    libffi_3*.deb
    openssl_1*.deb
    ca-cert*.deb

The python zip archive as used in youtubedl-android can be created using the following commands.

    cd debs
    dpkg-deb -xv python_*_x86_64.deb .
    dpkg-deb -xv libandroid-support_*_x86_64.deb .
    dpkg-deb -xv xz-utils_*_x86_64.deb .
    dpkg-deb -xv libffi_*_x86_64.deb .
    dpkg-deb -xv openssl_1*_x86_64.deb .
    dpkg-deb -xv ca-certificates_*deb .
    dpkg-deb -xv zlib_1*deb .
    cd data/youtubedl-android
    zip -r /tmp/python3_7_x86_64.zip usr/
    
NOTE: Version numbers can be different. Use <TAB> key for auto-fill.
