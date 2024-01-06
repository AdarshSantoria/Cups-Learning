# Building and Installing OpenPrinting CUPS on Ubuntu

## Installing Dependencies
```bash
sudo apt-get install autoconf build-essential libavahi-client-dev \
     libgnutls28-dev libkrb5-dev libnss-mdns libpam-dev \
     libsystemd-dev libusb-1.0-0-dev zlib1g-dev
```

## Forking [OpenPrinting/cups](https://github.com/OpenPrinting/cups) and Cloning the repository
```bash
git clone https://github.com/AdarshSantoria/cups
```

## Building
```bash
mkdir build
./configure --prefix=/home/adarsh/cups/build --enable-debug-printfs
make
sudo make install
```
- `mkdir build` & `--prefix=/home/adarsh/cups/build` : Saves all build files in a seperate folder
- `-enable-debug-printfs` : Configures the build with extra debug logging, enabling runtime debug messages (via `CUPS_DEBUG_xxx` variables) for issue diagnosis and troubleshooting.

## Testing
```bash
make test
```

## Running CUPS Daemon
```bash
sudo /home/adarsh/cups/build/sbin/cupsd -f
```
- `sudo /home/adarsh/cups/build/sbin/cupsd -f`: Starts the CUPS daemon in the foreground.
- `-f` :  Keeps the process in the foreground for interactive monitoring.
- This ensures that the self-compiled CUPS is running, overriding the system's default CUPS installation.

  # Building and Installing CUPS's libraries

  ## Qpdf
  ```
  git clone git@github.com:AdarshSantoria/qpdf.git
  cd qpdf
  cmake -S . -B build -DCMAKE_BUILD_TYPE=RelWithDebInfo
  cmake --build build
  cmake --install
  ```
- A dependency for other libraries
  
  ## libppd
  ```
  git clone git@github.com:AdarshSantoria/libppd.git
  cd libppd
  sudo apt-get install build-essential autoconf
  ./autogen.sh
  export CUPS_INSTALL_PATH=/home/adarsh/cups/build
  export CPPFLAGS="-I$CUPS_INSTALL_PATH/include"
  export LDFLAGS="-L$CUPS_INSTALL_PATH/lib"
  export PATH="$CUPS_INSTALL_PATH/bin:$PATH"
  ./configure --prefix=$CUPS_INSTALL_PATH
  make
  sudo make install
  ```
  
  ## libcups
  ```
  git clone git@github.com:AdarshSantoria/libcups.git
  cd libcups
  sudo apt-get install autoconf build-essential libavahi-client-dev \
     libgnutls28-dev libnss-mdns zlib1g-dev
  ./autogen.sh
  export CUPS_INSTALL_PATH=/home/adarsh/cups/build
  export CPPFLAGS="-I$CUPS_INSTALL_PATH/include"
  export LDFLAGS="-L$CUPS_INSTALL_PATH/lib"
  export PATH="$CUPS_INSTALL_PATH/bin:$PATH"
  ./configure --prefix=$CUPS_INSTALL_PATH
  make
  sudo make install
  ```

  ## libcupsfilters
  ```
  git clone git@github.com:AdarshSantoria/libcupsfilters.git
  cd libcupsfilters
  sudo apt-get install build-essential autoconf autopoint automake libtool
  sudo apt-get install libpoppler-cpp-dev poppler-utils libfontconfig1-dev liblcms2-dev mupdf-tools
  sudo apt-get install ghostscript
  sudo apt-get install libdbus-1-dev libjpeg-dev libpng-dev libtiff-dev libexif-dev
  sudo apt-get install fonts-dejavu-core
  ./autogen.sh
  export CUPS_INSTALL_PATH=/home/adarsh/cups/build
  export CPPFLAGS="-I$CUPS_INSTALL_PATH/include"
  export LDFLAGS="-L$CUPS_INSTALL_PATH/lib"
  export PATH="$CUPS_INSTALL_PATH/bin:$PATH"
  ./configure --prefix=$CUPS_INSTALL_PATH
  make
  sudo make install
  ```
