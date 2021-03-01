# PCemV17macOS
MacOS port of PCem low-level PC hardware emulator PCem V17. Experimental OpenGL 3 port. 

**Under macOS 10.14 (Mojave) and 10.15 (Catalina):**

Step 1: Install Xcode command-line tools

You need Xcode command-line tools from Apple in order to install Home Brew. You can install Xcode from the App Store or, when you run the Home Brew install script (step 2), it will install the command-line tools for you.

Step 2: Install Home Brew

Home Brew is the package manager for macOS that makes it easy to install the required packages needed for PCem to compile successfully. You can get it from https://brew.sh or run the following command from a Terminal shell:

/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"

Step 3: Install the required packages needed by PCem

In order to compile PCem on macOS you'll need sdl2, wxmac and openal-soft packages (Note: Later versions of macOS already have openal-soft so you may not need to install it using Home Brew). You can install theses with the following commands:

brew install sdl2

brew install wxmac

brew install openal-soft

Step 4: Download the Source Code

Download the source code from this repository and change directory to the PCem install folder.

Example: cd /PCemV17macOS-master

Step 5: Build PCem

Run the configuration script:

./configure --enable-release-build

If you want networking support:

./configure --enable-networking --enable-release-build

Assuming the command completes successfully run:

make -j4 -Wl,headerpad_max_install_names

This uses 4 threads in parallel and makes space for dylibs to be renamed later (in bundles).

This will take a while. You may see some warning messages during the make process but they do not seem to cause any issues with the compile. Once it completes you'll have the pcem executable file in the install folder. To start the program just run ./pcem from the terminal. You will need to obtain the required ROM files for the machine you want to emulate and need at least one valid ROM for pcem to start. These go in the roms folder located in the folder where PCem is installed.

**Under macOS 11 (Big Sur):**

1. Follow the same steps 1-4 as described above for Mojave & Catalina, but ommitting the command to install wxmac via Homebrew.

If wxmac is already installed, in Terminal run:

brew uninstall wxmac

Alternatively, you can go to usr/local/Cellar and move the wxmac folder elsewhere, unless/until you want the unmodified Homebrew version installed again.

2. Download wxmac from source: 

https://github.com/wxWidgets/wxWidgets/releases/download/v3.0.5.1/wxWidgets-3.0.5.1.tar.bz2

cd to the wxWidgets-3.0.5.1 folder and run:

./configure --prefix=/usr/local/Cellar/wxmac/3.0.5.1_1 --enable-clipboard --enable-controls --enable-dataviewctrl --enable-display --enable-dnd --enable-graphics_ctx --enable-std_string --enable-svg --enable-unicode --with-expat --with-libjpeg --with-libpng --with-libtiff --with-opengl --with-osx_cocoa --with-zlib --disable-precomp-headers --disable-monolithic --with-macosx-version-min=10.15 --disable-webview

Then run:

make install

This creates the wxmac libraries and the path to the config file is:

/usr/local/Cellar/wxmac/3.0.5.1_1/bin/wx-config

Download the PCemV17 source as above, cd into the folder and run the following configure command:

./configure --enable-networking --enable-release-build --with-wxdir=/usr/local/Cellar/wxmac/3.0.5.1_1/bin/

Then run:

make

This should result in the successfull compilation of the 'pcem' executable. Running it should produce the standard initial error message that no ROMs are present.
