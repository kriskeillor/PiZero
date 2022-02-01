# R Pi Zero W
2022-01-31
Journey-through-my-Zero, hopefully!

## Raspberry Pi Zero W installation, take 2

Created file "wpa_supplicant.conf" with the contents: 

```
country=US
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1

network={
    ssid="network-name"
    psk="network-passw"
}
```

Edited cmdline.txt to read (addition is `modules-load=dwc2,g_ether`, parameters are separated by spaces only):

```
console=serial0,115200 console=tty1 root=PARTUUID=e72b8fd1-02 rootfstype=ext4 fsck.repair=yes rootwait modules-load=dwc2,g_ether quiet init=/usr/lib/raspi-config/init_resize.sh

```

Was able to SSH in using Putty. Changed default password. Unable to change timezone, however.
/etc and /sbin seem like interesting directories to watch.
Also, /usr/share is a really interesting catch-all. Seems like low-level as well as user-edited content.

The command "/usr/share/python3/py3versions.py" is really interesting. It has a lot of tries and catches. Seems like a good template to study when working with programs that need to work with the OS in a fail-safe way. Running the file revealed my version of Python is 3.9.

Ran some basic updates:
```
sudo apt-get update
```
The command got the hooks, feteched the data, read the package lists, and then was done.

So, after up*dating*, it's time to up*grade*.
```
sudo apt-get upgrade
```

The only thing that changed was raspi-config. Now, to get it all working, I install & upgrade "pip3" (23 MB); "setuptools" was already installed. Also installed "adafruit-python-shell" which was only 65 KB. "adafruit-circuitpython-ssd1306", the package for the OLED, automatically trigged the latest "-framebuf" library. "adafruit-circuitpython-rfm9x" installed as V2.2.2.

"sudo apt-get install --upgrade" seems to be the four for one special. `pip3` uses the same general structure.

After downloading the example font and "rfm9x-raspberry-pi-setup.py", was able to get the hat displaying the demo code successfully.

The next need is to get the Zero W development sandbox working: https://raspberrypi.stackexchange.com/questions/36398/development-on-raspberry-pi

Not sure if I'll use sshfs or NFS, will probably ask Joe for some advice on that.