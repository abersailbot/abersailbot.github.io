# Introduction to Linux for Robotic Sailing

## Logging in
Connect to AberSailbot-dewi wifi
ssh test@192.168.40.1

SSH is built into Windows 10 April 2018 update. If you have an older version download [Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/) or [MobaXTerm](https://mobaxterm.mobatek.net/). 

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
  
 ### Filesystem structure
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
  w | Show who's logged in
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
  dd | Directly writes or reads data from a block device (memory card, disk or flash drive)
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
  
## Misc
  Directory | Description
  ------- | -----------
  date | Show current time and date
  ntpq -p | Show status of network time protocol. Used for syncing time from internet and GPS
  sudo halt | Shutdown
  sudo poweroff | Shutdown and turn off power (doesn't make a difference on a pi)
  sudo reboot | Reboots the system
  

## Redirects
  <command> > <filename>
  cat > output


## Pipes
  cat <filename> | more
  cat /etc/systemd/system.conf  | more
  head -n 20 <filename>
  tail -n 20 <filename>
  tail -20 <filename> 
  
## Compression
  zip -9 -r <zipfile> <directory>
  unzip -l <zipfile>
  unzip <zipfile>
  tar cvfz <targzfile> <directory>
  tar tvfz <targzfile>
  tar xvfz <targzfile>

### Sending compressed files over a network
  nc -l <listenport> | tar xvfz -
  tar cvfz - <directory> | nc <remotehost> <remoteport> 
  tar cvfz - <directory> | ssh <username>@<remotehost> 'tar xvfz -'

## Finding things
  grep <some text> <filename>
  ps aux | grep <some process>
  dpkg -l | grep <some package>
  find <directory name> -name <filename>
  find <directory name> -name <filename> -exec <some action>

