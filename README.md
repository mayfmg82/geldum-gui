# Geldum GUI

Copyright (c) 2014-2017, The Monero Project
Copyright (c) 2018-2018, The Geldum Project

## Development Resources

- Web: [geldum.org](http://geldum.org)
- Geldum Core Github: [https://github.com/geldumproject/geldum](https://github.com/geldumproject/geldum)
- Geldum GUI Wallet: [https://github.com/geldumproject/geldum-gui](https://github.com/geldumproject/geldum-gui)

## About this Project

This is the GUI for the [core Geldum implementation](https://github.com/geldumproject/geldum). It is open source and completely free to use without restrictions, except for those specified in the license agreement below. There are no restrictions on anyone creating an alternative implementation of Geldum that uses the protocol and network in a compatible manner.

As with many development projects, the repository on Github is considered to be the "staging" area for the latest changes. Before changes are merged into that branch on the main repository, they are tested by individual developers in their own branches. It is generally a better idea to use a tagged release for stability.

## Supporting the Project

Geldum development can be supported directly through donations.
If you want to Donate, just join either our Discord Channel (http://discord.gg/vBjwx6J) or Telegram Group (http://t.me/geldum)

## License

See [LICENSE](LICENSE).

## Installing Geldum Core from a Package

Packages are available for Linux / Windows / OsX

Packaging for your favorite distribution would be a welcome contribution!

## Compiling Geldum Core + Geldum GUI from Source

### On Linux:


1. Install Geldum dependencies

  - For Ubuntu and Mint

	`sudo apt install build-essential cmake libboost-all-dev miniupnpc libunbound-dev graphviz doxygen libunwind8-dev pkg-config libssl-dev`

  - For Gentoo

	`sudo emerge app-arch/xz-utils app-doc/doxygen dev-cpp/gtest dev-libs/boost dev-libs/expat dev-libs/openssl dev-util/cmake media-gfx/graphviz net-dns/unbound net-libs/ldns net-libs/miniupnpc sys-libs/libunwind`

2. Grab an up-to-date copy of the geldum-gui repository

	`git clone https://github.com/geldumproject/geldum-gui.git`

3. Go into the repository

	`cd geldum-gui`

4. Install the GUI dependencies

  - For Ubuntu 16.04 x86

	`sudo apt-get install qtbase5-dev qt5-default qtdeclarative5-dev qml-module-qtquick-controls qml-module-qtquick-xmllistmodel qttools5-dev-tools qml-module-qtquick-dialogs`

  - For Ubuntu 16.04+ x64

    `sudo apt-get install qtbase5-dev qt5-default qtdeclarative5-dev qml-module-qtquick-controls qml-module-qtquick-xmllistmodel qttools5-dev-tools qml-module-qtquick-dialogs qml-module-qt-labs-settings libqt5qml-graphicaleffects`

  - For Linux Mint 18 "Sarah" - Cinnamon x64

    `sudo apt install qml-module-qt-labs-settings qml-module-qtgraphicaleffects`

  - For Gentoo

    `sudo emerge dev-qt/qtcore:5 dev-qt/qtdeclarative:5 dev-qt/qtquickcontrols:5 dev-qt/qtquickcontrols2:5 dev-qt/qtgraphicaleffects:5`

  - Optional : To build the flag `WITH_SCANNER`

    - For Ubuntu and Mint

      `sudo apt install qtmultimedia5-dev qml-module-qtmultimedia libzbar-dev`

    - For Gentoo

      The *qml* USE flag must be enabled.

      `emerge dev-qt/qtmultimedia:5 media-gfx/zbar`

5. Build the GUI

  - For Ubuntu and Mint

	`./build.sh`

  - For Gentoo

    `QT_SELECT=5 ./build.sh`

The executable can be found in the build/release/bin folder.

### On OS X:

1. Install Xcode from AppStore
2. Install [homebrew](http://brew.sh/)
3. Install [geldum](https://github.com/geldumproject/geldum) dependencies:

  `brew install boost --c++11`

  `brew install openssl` - to install openssl headers

  `brew install pkgconfig`

  `brew install cmake`

  `brew install qt5`  (or download QT 5.8+ from [qt.io](https://www.qt.io/download-open-source/))

  If you have an older version of Qt installed via homebrew, you can force it to use 5.x like so:
  
  `brew link --force --overwrite qt5`

5. Add the Qt bin directory to your path

    Example: `export PATH=$PATH:$HOME/Qt/5.8/clang_64/bin`

    This is the directory where Qt 5.x is installed on **your** system

6. Grab an up-to-date copy of the geldum repository

  `git clone https://github.com/geldumproject/geldum-gui.git`

7. Go into the repository

  `cd geldum-gui`

8. Start the build

  `./build.sh`

The executable can be found in the `build/release/bin` folder.

**Note:** Workaround for "ERROR: Xcode not set up properly"

Edit `$HOME/Qt/5.8/clang_64/mkspecs/features/mac/default_pre.prf`

replace
`isEmpty($$list($$system("/usr/bin/xcrun -find xcrun 2>/dev/null")))`

with
`isEmpty($$list($$system("/usr/bin/xcrun -find xcodebuild 2>/dev/null")))`

More info: http://stackoverflow.com/a/35098040/1683164


### On Windows:

1. Install [msys2](http://msys2.github.io/), follow the instructions on that page on how to update packages to the latest versions

2. Install geldum dependencies as described in [geldum documentation](https://github.com/geldumproject/geldum) into msys2 environment
   **As we only build application for x86, install only dependencies for x86 architecture (i686 in package name)**
   ```
   pacman -S mingw-w64-i686-toolchain make mingw-w64-i686-cmake mingw-w64-i686-boost

   ```

3. Install git into msys2 environment

    ```
    pacman -S git
    ```

4. Install Qt5 from [official site](https://www.qt.io/download-open-source/)
   - download unified installer, run and select following options:
       - Qt > Qt 5.7 > MinGW 5.3.0 32 bit
       - Tools > MinGW 5.3.0
   - continue with installation

5. Open ```MinGW-w64 Win32 Shell``` shell

   ```%MSYS_ROOT%\msys2_shell.cmd -mingw32```

   Where ```%MSYS_ROOT%``` will be ```c:\msys32``` if your host OS is x86-based or ```c:\msys64``` if your host OS
   is x64-based

6. Install the latest version of boost, specificly the required static libraries
    ```
    cd
    wget http://sourceforge.net/projects/boost/files/boost/1.63.0/boost_1_63_0.tar.bz2
    tar xjf boost_1_63_0.tar.bz2
    cd boost_1_63_0
    ./bootstrap.sh mingw
    ./b2 --prefix=/mingw32/boost --layout=tagged --without-mpi --without-python toolset=gcc address-model=32 variant=debug,release link=static threading=multi runtime-link=static -j$(nproc) install
    ```

7. Clone repository
    ```
    cd
    git clone https://github.com/geldumproject/geldum-gui.git
    ```

8. Build the GUI
    ```
    cd geldum-gui
    export PATH=$(ls -rd /c/Qt/5.[6,7,8]/mingw53_32/bin | head -1):$PATH
    ./build.sh
    cd build
    make deploy
    ```

The executable can be found in the ```.\release\bin``` directory.
