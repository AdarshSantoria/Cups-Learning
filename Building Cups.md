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
./configure
make
sudo make install
```

## Testing
```bash
make test
```
