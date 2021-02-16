# PCemV17macOS
PCem for macOS + OpenGL 3.0 support

**NOTE: Currently PCem will not compile on macOS 11 Big Sur. Follow the instructions below if you are running Mojave (10.14) or Catalina (10.15). There is a work-around to get your PCem you compiled in Mojave/Catalina running on Big Sur, which is detailed separately below.

**NOTE: There are reports of severely degraded performance from the dynamic recompiler in v17 of PCem, which seems to be only affect macOS and perhaps only certain processor configurations. This is in the process of being investigated, but if you experience issues it is suggested that you revert to v16 for the time being.

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

Step 3: Download the Source Code

Download the source code from this repository and change directory to the PCem install folder.

Example: cd /PCemV16macOS-master

Step 3: Build PCem

Run the configuration script:

./configure --enable-release-build

If you want networking support:

./configure --enable-networking --enable-release-build

Assuming the command completes successfully run:

make

This will take a while. You may see some warning messages during the make process but they do not seem to cause any issues with the compile. Once it completes you'll have the pcem executable file in the install folder. To start the program just run ./pcem from the terminal. You will need to obtain the required ROM files for the machine you want to emulate and need at least one valid ROM for pcem to start. These go in the roms folder located in the folder where PCem is installed.




**To run PCem on Big Sur (confirmed as working in 11.2.1), follow these exact steps*

In Mojave or Catalina:

(if you never installed wxmac with Homebrew, skip step 1)

1. In Terminal run:

brew uninstall wxmac

2. Download: 

https://github.com/wxWidgets/wxWidgets/releases/download/v3.0.5.1/wxWidgets-3.0.5.1.tar.bz2

cd to the wxWidgets folder and run:

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

On Big Sur:

Follow steps 1-3 as above, to create an identical installation of wxmac on your Big Sur installation. Alternatively, if you have access to dual installs of macOS, you can copy the wxmac you installed under usr/local/Cellar in Mojave/Catalina and move it to the same location in your Big Sur installation.

Copy across your Pcem executable from Mojave/Catalina and it should run fine, producing the same ROM error, which means you are in business!

If a lack of webview functionality in wxmac causes problems for other packages, you can just move the folder temporarily, or delete it and re-install the standard package using Homebrew.
