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
