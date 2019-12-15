# DualVirtualDisplay-VNC-Linux

A bash script to use your VNC client as a secondry display by making a virtual display in your computer.

## Get ModeLine

use [gtf](https://linux.die.net/man/1/gtf) followed by the required screen resolution and refresh rate to get ModeLine

```bash
gtf 1280 1204 60
```

## Create New Mode

copy the output after "ModeLine" and pass it to xrandr with flag --newmode

```bash
xrandr --newmode "1280x1024_60.00"  108.88  1280 1360 1496 1712  1024 1025 1028 1060  -HSync +Vsync
```

## Add Mode

pass "Display Name" and "Mode Name" after flag --addmode to xrandr.

```bash
xrandr --addmode HDMI-1-1 1280x1024_60.00
```

## Create output

use "--left-of" or "--right-of" flag to place the virtual display to the left or right of your primary display i.e eDP-1-1 in this case.

```bash
xrandr --output HDMI-1-1 --mode 1280x1024_60.00 --left-of eDP-1-1
```

## Start VNC Server

We are using [x11vnc](https://linux.die.net/man/1/x11vnc) in our case.
Install it by using

```bash
sudo apt install x11vnc
```
Pass ModeName followed by offset and flag -clip to x11vnc.
```bash
x11vnc -clip 1280x1024+0+0
```

## That's All

Connect to the vnc server on your device.

#### Done !
