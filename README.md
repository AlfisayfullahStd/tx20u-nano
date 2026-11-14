Here is the simplified and direct `README.md` tailored specifically for the **TP-Link Archer TX20U Nano**:


# Realtek RTL8852BU Driver (Optimized for TP-Link Archer TX20U Nano)

Linux driver for the **TP-Link Archer TX20U Nano** USB Wi-Fi Adapter (and other RTL8852BU/RTL8832BU chipsets).

---

## 1. Install Dependencies
Make sure your system has the required build tools and kernel headers installed:

**Ubuntu / Debian / Armbian:**
```bash
sudo apt update
sudo apt install make gcc linux-headers-$(uname -r) build-essential git
```

## 2. Register USB ID (TP-Link TX20U Nano)

Before compiling, add the `35bc:0108` USB ID to the driver source code so it recognizes your adapter:

```bash
git clone [https://github.com/lwfinger/rtl8852bu.git](https://github.com/lwfinger/rtl8852bu.git)
cd rtl8852bu

# Automatically inject the USB ID into the driver source
sed -i '/static struct usb_device_id rtw_usb_id_tbl/a \t{USB_DEVICE(0x35bc, 0x0108), .driver_info = RTL8852B},' os_dep/linux/usb_intf.c

```

---

## 3. Compile & Install

### For Standard x86 / PC:

```bash
make clean
make
sudo make install
sudo modprobe 8852bu

```

### For ARM64 / AArch64 (Jetson Tegra / Raspberry Pi):

```bash
make clean
make ARCH=arm64
sudo make ARCH=arm64 install
sudo modprobe 8852bu

```

---

## 4. Optional: DKMS Setup (Automatic Kernel Updates)

To prevent losing the driver when your system updates the kernel:

```bash
sudo dkms add .
sudo dkms build rtl8852bu -v 1.15.0.1
sudo dkms install rtl8852bu -v 1.15.0.1
sudo modprobe 8852bu

```

---

## 5. Verify Installation

Run the following command to check if your new Wi-Fi interface is active:

```bash
iwconfig
# or
ip a

```

```

```
