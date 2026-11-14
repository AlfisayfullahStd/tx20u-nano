# Realtek RTL8852BU Driver for TP-Link Archer TX20U Nano

Linux driver for the **TP-Link Archer TX20U Nano** USB Wi-Fi adapter, based on the Realtek RTL8852BU driver.

The adapter USB ID `35bc:0108` is already included in this repository. No manual source modification is required.

## 1. Install dependencies

On Ubuntu, Debian, or Armbian:

```bash
sudo apt update
sudo apt install make gcc linux-headers-$(uname -r) build-essential git
```

## 2. Download the source

Clone this repository and enter its directory:

```bash
git clone https://github.com/AlfisayfullahStd/tx20u-nano.git
cd tx20u-nano
```

## 3. Compile and install

### Standard x86 / PC

```bash
make clean
make
sudo make install
sudo modprobe -r 8852bu 2>/dev/null || true
sudo modprobe 8852bu
```

### ARM64 / AArch64

```bash
make clean
make ARCH=arm64
sudo make ARCH=arm64 install
sudo modprobe -r 8852bu 2>/dev/null || true
sudo modprobe 8852bu
```

## 4. Verify installation

Check that the adapter is detected and that a wireless interface is available:

```bash
lsusb -d 35bc:0108
iw dev
ip link
```
