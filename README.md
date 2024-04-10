# android-on-linux
## Stable Connenction of Android to Linux
* Merit to: [Archlinux Wiki](https://wiki.archlinux.org/title/Android_Debug_Bridge) 
* Symptom-s: You connect your Android-Device to your Linux and the connection switch continuosily ON & OFF

### 1. Install Prerequisite 

`paru -S android-sdk-platform-tools`

* Optional Install-s:

` paru -S qtscrcpy`

### 2. Figure out device IDs
* Use first `lsusb` to detect all ubs-devices and recognize the Vendor-Name.
* Once you know the Vendor name use `lsusb -v` to get exactly `vendor id:` & `product id:` , e.g.:

```
vendor id: 0x2717

product id: 0xff48
```

### 3. Make a udev-rule as for any device
#### 3.1. Solution:
1. Create a file with nano as follow:

`sudo nano /etc/udev/rules.d/51-android.rules` 

2. Add following content: 

```
SUBSYSTEM=="usb", ATTR{idVendor}=="[0x2717]", MODE="0660", GROUP="adbusers", TAG+="uaccess"
SUBSYSTEM=="usb", ATTR{idVendor}=="[0x2717]", ATTR{idProduct}=="[0xff48]", SYMLINK+="android_adb"
SUBSYSTEM=="usb", ATTR{idVendor}=="[0x2717]", ATTR{idProduct}=="[0xff48]", SYMLINK+="android_fastboot"

```

3. Let an empty line at end of file, save with [CTRL+O] & close with [CTRL+X]

* **NOTE:** A file to copy with sudo-privilieges is already present, modify with your own `vendor id:` & `product id:`, save the file & copy it at destination replacing the underscore `_` with a slash `/`.

#### 3.2. Solution:
1. Create a file with nano as follow:

`sudo nano /etc/udev/rules.d/71-android.rules` 

2. Add following content: 

```
SUBSYSTEMS=="usb", ATTRS{idVendor}=="0x2717", ATTRS{idProduct}=="0xff48", MODE="0660", TAG+="uaccess"

```

3. Let an empty line at end of file, save with [CTRL+O] & close with [CTRL+X]

* **NOTE:** A file to copy with sudo-privilieges is already present, modify with your own `vendor id:` & `product id:`, save the file & copy it at destination replacing the underscore `_` with a slash `/`.


✅ Done & Enjoy❗️







