# What is it
* Single board computer
* Cheap, under £30
* Runs Linux, operating system stored on SD card
* Power of desktop computer from early 2000s
* 512MB or 1GB RAM
* Lots of I/O facilities
* Aimed as teaching platform, used heavily by roboticists, hobbyists, makers etc

## Versions of the Pi

### Pi B

Original Pi, 2 USB, 256MB/512MB RAM, full size SD card, single core 

![Original Pi B](https://elinux.org/images/thumb/f/f4/RaspiFront.JPG/250px-RaspiFront.JPG)

### Pi A

Same as B, but no ethernet, one USB port

### Pi B+

Switched to microSD, 4 USB ports, bigger IO interface, better voltage regulator, same processor as original.
Lowest power consmuption of the Raspberry Pi B's. 

![Pi B+](https://www.raspberrypi.org/app/uploads/2017/05/Raspberry-Pi-Model-B-overhead-1-1540x1080.jpg)

### Pi 2 B

Same form factor as model B+. Faster quad core CPU 900 MHz CPU, 1GB RAM.
More power hungry than B+

![Pi 2](https://www.raspberrypi.org/app/uploads/2017/05/Raspberry-Pi-2-overhead-1-1576x1080.jpg)

### Pi 3 B

Same form factor as model B+. Newer CPU, 64 bit capable but no used by Raspbian OS. Built in WiFi and Bluetooth.
More power hungry than 2 or B+.

![Pi 3](https://www.raspberrypi.org/app/uploads/2017/05/Raspberry-Pi-3-hero-1-1571x1080.jpg)

### Pi 3 B+

Better CPU thermal management, faster clock speed. Faster WiFi. Faster ethernet. Power over Ethernet.
![Pi 3 B+](https://elinux.org/images/thumb/d/dd/RPi3B%2B500x334.jpg/250px-RPi3B%2B500x334.jpg)


### Pi Zero

Smaller form factor. Half the size of the standard Pi. Only costs £5. 
Same CPU as original Pi B/A, slightly faster clock speed. 512 MB RAM.
No ethernet, micro HDMI and micro USB host.

![Pi Zero](https://www.raspberrypi.org/app/uploads/2017/05/PI-Zero-W-1-1620x1080.jpg)


### Pi Zero W
Wifi/bluetooth enabled Pi Zero.

### Performance Comparison 

![Performance Graph](https://www.raspberrypi.org/magpi/wp-content/uploads/2016/02/Sysbench.png)


# I/O capabilities 

## 40 pin connector

![GPIO connector](https://www.element14.com/community/servlet/JiveServlet/downloadImage/102-78315-19-229602/762-644/GPIO-pinout-and-rpi.jpg)

* GPIO = general purpose I/O, switch on/off pin or read on/off state
* Also useful serial port, I2C, SPI and PWM.
* We only use serial for GPS

## GPIO control from a filesystem

```#!/bin/sh```

```echo "4" > /sys/class/gpio/export```

```echo "out" > /sys/class/gpio/gpio4/direction```

```echo 1 > /sys/class/gpio4/value```

# Flashing an OS

 * The operating system has to be copied to an SD card.
 * Two partitions: 
 * /boot contains firmware, config.txt, Linux kernel, cmdline.txt (kernel config)
 * / contains a standard Linux system
 * Imagefile contains both partitions
 * Write it to an SD card with dd or ethcher
 * Image usually 1,2 or 4GB. 
 * After install expand with raspiconfig to fill whole SD card.
 * OS can be backed up in the same way.
 * Download images from [https://www.raspberrypi.org/downloads/raspbian/]
 
 
# Common Faults
 * SD card corruption.  Mount on a PC and run fsck. 
 * SD card failure, often after pulling out power without proper shutdown.
 * SD card becomes read only, but appears to be writable until reboot
 * Bent pins
 * USB connector comes loose
 
 
# Useful programs
* raspiconfig - Configures various things
* pinout - gpiozero's pinout program, shows a pinout map for the current Pi
