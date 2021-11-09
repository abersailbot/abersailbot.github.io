# Introduction to Linux for Robotic Sailing

# Raspberry Pi -  What is it
* Single board computer
* Cheap, under £30
* Runs Linux, operating system stored on SD card
* Power of desktop computer from early 2000s
* 512MB to 4GB of RAM
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

### Pi 4 B

USB 3, faster ethernet, 1/2/4GB RAM options, dual display, faster processor.
![Pi 4 B](https://www.seeedstudio.site/media/catalog/product/cache/ab187aaa5f626ad16c8031644cd2de5b/4/g/4g.png)


### Pi Zero

Smaller form factor. Half the size of the standard Pi. Only costs £5. 
Same CPU as original Pi B/A, slightly faster clock speed. 512 MB RAM.
No ethernet, micro HDMI and micro USB host.

![Pi Zero](https://www.raspberrypi.org/app/uploads/2017/05/PI-Zero-W-1-1620x1080.jpg)


### Pi Zero W
Wifi/bluetooth enabled Pi Zero.

### Pi Zero 2W
Faster quad core version of the Pi Zero, comparable to performance of Pi 3, but only 512MB of RA.

### Performance Comparison 

![Performance Graph](https://www.raspberrypi.org/magpi/wp-content/uploads/2016/02/Sysbench.png)


## I/O capabilities 

### 40 pin connector

![GPIO connector](https://www.element14.com/community/servlet/JiveServlet/downloadImage/102-78315-19-229602/762-644/GPIO-pinout-and-rpi.jpg)

* GPIO = general purpose I/O, switch on/off pin or read on/off state
* Also useful serial port, I2C, SPI and PWM.
* We only use serial for GPS

### GPIO control from a filesystem

```#!/bin/sh```

```echo "4" > /sys/class/gpio/export```

```echo "out" > /sys/class/gpio/gpio4/direction```

```echo 1 > /sys/class/gpio4/value```

## Flashing an OS

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
 
 
## Common Faults
 * SD card corruption.  Mount on a PC and run fsck. 
 * SD card failure, often after pulling out power without proper shutdown.
 * SD card becomes read only, but appears to be writable until reboot
 * Bent pins
 * USB connector comes loose
 
 

## Logging in
1. Connect to AberSailbot-dewi wifi
2. ssh test@192.168.40.1

SSH is built into Windows 10 April 2018 update. If you have an older version download [Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/) or [MobaXTerm](https://mobaxterm.mobatek.net/). 


# Linux Commands

  Command | Description
  -------- | -----------
  cd (directory) | Changes to (directory)
  cd / | Changes to root directory
  pwd | Show current working directory 
  mkdir (directory) | Makes a directory
  rmdir (directory) | Removes a directory
  ls  | list all files in current directory
  ls -l  | list all files with their times/dates, sizes and permissions
  ls -a | list all hidden files
  cp (source file) (destination directory) | Copies (source file) to (destination directory), use "." to indicate current directory
  mv (source file/directory) (destination directory) | Moves (source file) to (destination directory)
  ps aux | Show all processes running on the system
  ps -u (username) | Show all processes running for a given user
  top | Shows which process is consuming the most CPU. Press q to exit.
  service (servicename) status | Show status of a system process. 
  scp (username)@(hostname):(remote dir name) (destination directory) | Copies a file from a remote host use "." to indicate current directory



## Exercises

1. Login to the Pi
2. Create a directory with your user ID using mkdir
3. Change to that directory with cd
4. Copy /etc/boatd-config.yaml to your directory using cp
5. Edit your copy of boatd-config.yaml with nano (or your favourite text editor). Change the waypoints file to "waypoint_file: /home/pi/<your user id>/waypoints"
6. Open a new terminal ON YOUR COMPUTER, copy your version of boatd back to your computer using scp.
7. Edit the file on YOUR COMPUTER and change the "home_position:" coordinates to 52.41594,-4.06575
8. Copy your new config back to the boat using scp.

# Many more useful commands

## Filesystem commands

  Command | Description
  -------- | -----------
  mount | Show mounted filesystems
  df -h | Show how much disk space is free, with human readable units
  du -h (directory) | Show how much disk is used by (directory)
  cp (file) (directory) | Copies (file) to (directory)
  mv (file) (directory) | Moves (file) to (directory)
  rm (file)  | Deletes (file)
  cd (directory) | Changes to (directory)
  cd / | Changes to root directory
  pwd | Show current working directory 
  mkdir (directory) | Makes a directory
  rmdir (directory) | Removes a directory
  rm -rf (directory) | Deletes a directory
  ls  | list all files in current directory
  ls -l  | list all files with their times/dates, sizes and permissions
  ls -a | list all hidden files
  ls -lrt | list all files with metadata, in reverse time order
  ln -s (filename) (linkname) | Makes a symbolic link from (filename) to (linkname)
  ln (filename) (linkname) | Makes a hard link from (filename) to (linkname), both original and link look like a real file.
  chmod 700 (filename) | Give owner read, write and execute permission, give nobody else anything.
  chmod 600 (filename) | Give owner read and write permission, give nobody else anything.
  chmod 754 (filename) | Give owner read and write permission, give group read and execute, everyone else read only.
  chmod u+w (filename) | add write permission for the owner
  chmod g+w (filename) | add write permission for the group
  chmod o+w (filename) | add write permission for everyone else
  
  Permission numbers 
  * read = 4
  * write = 2
  * execute = 1
  
  Characters
  * u = user
  * g = group
  * o = others
  * a = everyone
  * r = read
  * w = write
  * x = execute


## Filesystem structure
 
   Directory | Description
   ------- | -----------
   / | Root of the filesystem, contains everything else even if its on a different disk
   /home | Home directories for user data
   /etc | Configuration files
   /bin | Core programs
   /sbin | Core programs that only root should run
   /usr | User installed software (using the package manager)
   /usr/bin | Executables for user installed software
   /usr/lib | Libraries for user installed software
   /usr/local | Software installed by the user without a package manager
   /usr/sbin | User installed executables for root to use
   /lib | Core system libraries
   /var | System variables and log files 
   /var/log | Log files
   /tmp | temporary files, often a ram disk on Raspberry Pi's
   
   #### Virtual filesystems
   
   These are special filesystems which don't contain real files but represent the internal state of the system or the hardware.
  
   Directory | Description
   ------- | -----------
   /sys | Special system devices, these aren't really files but a psuedo filesystem which controls things in the system. On a Pi this directly controls IO pins. Also things like wifi on/off, battery, screen brightness, CPU speed controls etc.
   /dev | System I/O devices, read or writing to these allows us to send and receive data from some hardware.
   /proc | Process control and kernel filesystem. Contains a sub directory for each process + loads for controlling kernel parameters. 
   


## Processes

  Directory | Description
  ------- | -----------
  ps aux | Show all processes running on the system
  ps -u (username) | Show all processes running for a given user
  top | Shows which process is consuming the most CPU. Press q to exit.
  htop | Fancy version of top
  service (servicename) status | Show status of a system process. 
  sudo service (servicename) stop | Stop a service, must be root
  sudo service (servicename) start | Start a service, must be root
  sudo service (servicename) restart | Restarts a service, must be root
  sudo service (servicename) reload | Reloads a service's config files, must be root
  systemctl status (servicename) | Show status of a system process (systemd). 
  sudo systemctl stop (servicename) | Stop a service (systemd), must be root
  sudo systemctl start (servicename) | Start a service (systemd), must be root
  sudo systemctl restart (servicename) | Restarts a service (systemd), must be root
  sudo systemctl reload (servicename) | Reloads a service's config files (systemd), must be root
  sudo systemctl disable (servicename) | disables the systemd service running on startup
  sudo systemctl enable (servicename) | enables the systemd service to run on startup
  ctrl c | press this to stop most programs running
  ctrl z | press this to suspend a program. 
  fg | continue suspended program in the foreground
  bg | continue suspended program in the background
  kill (processid) | requests a process terminate, (processid) is a number shown in the PID column in ps/top/htop.
  killall (processname) | terminate a process of the name (processname)
  kill -KILL (processid) | force a process to stop, it will not be given a chance to save anything
  killall -KILL (processname) | kill a process by name
  (program) & | run (program) in the background. Its output will still appear on your screen,possibly on top of other things

## File transfer

  Directory | Description
  ------- | -----------
  scp (filename) (username)@(hostname):(remote dir name) | Copies a file to a remote host
  scp (filename) (username)@(hostname): | Copies a file to (username's) home directory on a remote host
  scp (username)@(hostname):(remote dir and file name) (filename) | Copies a file from a remote host

## Networking

  Directory | Description
  ------- | -----------
  curl http://localhost | Download's a webpage displays it on screen
  wget http://localhost | Download's a webpage and saves it as a file
  ifconfig | Show network interfaces, ethX are wired, wlanX are wireless, lo is loopback
  iwconfig | Show wifi config
  ip route show | Show system routing table
  nc (hostname) (port) | Connects to a network service on a remote host. 
  cat /etc/udev/rules.d/10-network-device.rules | Udev rules for network devices, sets interface names
  sudo dhclient (interface name) | Start a DHCP client to automatically obtain an IP address for an interface. /etc/network/interfaces causes this to happen automatically on some interfaces.
  ping (hostname) | Send a message to a remote host to see if its online
  host (hostname) | Resolves the IP address from a hostname. Requires internet access.
  
## Packaging

  Directory | Description
  ------- | -----------
  dpkg -l | List all installed packages 
  dpkg -L (packagename)  | List all filenames in (packagename)
  apt search (packagename) or apt-cache search (packagename) | Look for packages which can be installed. Shows near matches and substrings.
  sudo apt install (packagename) or apt-get install (packagename) | Install a package, name must be exact. Requires internet.
  sudo apt update | Updates the list of packages available.
  sudo apt upgrade | Upgrades any packages which have newer versions available.
  sudo apt dist-upgrade | On regular Linux systems upgrades the kernel and does major updates to some packages. Might not upgrade a Raspberry Pi kernel.

## User management

  Directory | Description
  ------- | -----------
  w | Show who's logged in, system uptime and load average.
  sudo adduser (username) | Add a new user (requires root)
  groups (username) | Show which groups a user is in.
  sudo usermod -aG (groupname(s)) (username) | Add's a user to some groups. Anyone wanting access to serial ports must be in dialout group.

## Hardware

  Directory | Description
  ------- | -----------
  dmesg | Show kernel messages, useful for diagnosing problems
  lsusb | List all USB devices attached
  lsblk | List all storage devices
  lscpu | List all CPUs
  free | Show how much RAM is free
  cat /proc/meminfo | Show info about the RAM
  cat /proc/cpuinfo | Show info about the CPUs
  cat /proc/partitions | Show the partitions of all disks on the system
  fdisk -l (devicename) | Show the parttions on (devicename)
  dd if=(imagefile) of=(output device)| Directly writes raw data to a block device (memory card, disk or flash drive) from an image file. Useful for reflashing SD cards. Reverse if and of to backup the SD card. Use with caution, can wipe out data if not careful. Always double check device names with lsblk.
  stty -F(serial port) | Show settings of a serial port
  screen (serialport) (baud rate) | Connects to a serial port. Press CTRL a then k to exit.
  cgps | Fancy command line GPS status
  gpscat | Simple command line GPS state info
  udevadm monitor | Show events from hotplugging devices
  ls -l /dev/serial/by-id | List all serial devices by ID
  cat /etc/udev/rules.d/52-arduino.rules | Special Udev rules for Arduino, creates a symlink in /dev/arduino to whatever serial port name the arduino has
  
### GPIO control
  
  Directory | Description
  ------- | -----------
  sudo echo 18 > /sys/class/gpio/export | Allow access to pin 18
  sudo echo out > /sys/class/gpio/gpio18/direction  | Set pin 18 as an output
  sudo echo 1 > /sys/class/gpio/gpio18/value | Turn on pin 18
  
### Raspberry Pi Specific

  Directory | Description
  ------- | -----------
  sudo raspi-config | Raspberry pi hardware configuration utility
  sudo rpi-update | Updates firmware (and kernels??)
  cat /boot/cmdline.txt  | Raspberry Pi kernel command line config
  cat /boot/config.txt  | Raspberry Pi hardware configuration, set hdmi_force_hotplug=1
  vcgencmd | Controls lots of special hardware things. 
  vcgencmd measure_temp | measures CPU temperature
  pinout | gpiozero's pinout program, shows a pinout map for the current Pi

  
## Misc

  Directory | Description
  ------- | -----------
  date | Show current time and date.  Can also set date if run as root.
  ntpq -p | Show status of network time protocol. Used for syncing time from internet and GPS
  ntpdate (ntpserver) | force the time to be updated from (ntpserver). ntpd can't be running when this happens.
  sudo halt | Shutdown
  sudo poweroff | Shutdown and turn off power (doesn't make a difference on a pi)
  sudo reboot | Reboots the system
  export PATH=$PATH:/home/me/myprogram | adds /home/me/myprogram to the PATH environment variable
  echo $PATH | shows the contents of the PATH environment variable
  env | shows all environment variables
  diff (file1) (file2) | show the differences between two files, diff -c has nicer formatting.
  

## Redirects

  Directory | Description
  ------- | -----------
  (command) > (filename) | Sends the output from (command) to (filename) and overwrites (filename)
  (command) >> (filename) | Sends the output from (command) to (filename) and appends (filename)
  ls > output | sends the output of ls to the file output
  (command) 2>&1 | Sends output of standard error to standard out.
  (command) > /dev/null | sends the output of a command to /dev/null which just discards it. Useful if you want to throw away and ignore the output instead of having it clutter up the screen.
  


## Pipes

  cat (filename) | more
  cat /etc/systemd/system.conf  | more
  
  Directory | Description
  ------- | -----------
  head -n 20 (filename) | Displays the first 20 lines
  tail -n 20 (filename) | Displays the last 20 lines
  tail -20 (filename) | Also displays the last 20 lines
    
  
## Compression

  Directory | Description
  ------- | -----------
  zip -9 -r (zipfile) (directory) | zip all files in (directory) and store them in (zipfile)
  unzip -l (zipfile) | list the contents of (zipfile)
  unzip (zipfile) | extract the contents of (zipfile)
  tar cvfz (targzfile) (directory) | create a compressed tar archive of (directory) and store it in (targzfile). These usually have the extension .tar.gz or .tgz
  tar tvfz (targzfile) | List contents of a tar.gz file
  tar xvfz (targzfile) | Extract a tar.gz file

### Sending compressed files over a network

On the receiving system, run nc and pipe its output to tar xvfz.
```nc -l <listenport> | tar xvfz -```

On sending system run tar cvfz and send its output to nc. 
Note that - means send output to the screen/pipe.
```tar cvfz - <directory> | nc <remotehost> <remoteport> ```

Send output of tar to SSH, have SSH run the extract command on the remote system. 
```tar cvfz - <directory> | ssh <username>@<remotehost> 'tar xvfz -'```

## Finding things

  Directory | Description
  ------- | -----------
  grep (some text) (filename) | Finds text (and regular expressions) in a file
  ps aux \| grep (some process) |  Search the output of ps aux for text
  dpkg -l \| grep (some package) | Search the output of dpkg -l for a package name
  find (directory name) -name (filename) | finds (filename) in (directory name), can include wildcards,e.g. a* means all files beginning with an a
  find (directory name) -name (filename) -exec (some action) {} \\; | finds files and runs a program on them. {} is substitued for the filename.
  
## Text manipulation

  Directory | Description
  ------- | -----------
  cat (filename) \| cut -b 2-3 | Show the second and third character of each line in a file
  cat (filename) \| awk '{print $1}' | Show everything up to the first space on each line of a file
  cat (filename) \| awk -F, '{print $1}' | Show everything up to the first comma on each line of a file
  cat (filename) \| sed 's/a/A/' | Change the first lower case a to an upper case A on each line of a file
  cat (filename) \| sed 's/a/A/g' | Change all lower case a's to an upper case A's on each line of a file
  cat (filename) \| tr -d '\n' | deletes all newlines in each line of a file
  
  cut,awk,sed and tr can all work on input from both a pipe or they can be given a filename.
  tr -d '\n' (filename) is the same as cat (filename) | tr -d '\n'
   
## Text Editors
  
  Directory | Description
  ------- | -----------
     vi    | Very simple editor, a bit strange to use as it has command and insert modes. Press escape to switch between them. i inserts, a appends, :wq saves and exist,:q! exits without saving.
      emacs | An operating system with a built in text editor. Press ctrl x ctrl c to exit.
      nano | More intuitive for beginners but less powerful than vi or emacs. Press ctrl x to exit.
      
   
      
  
 
