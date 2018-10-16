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
  vcgencmd | Controls lots of special hardware things. 
  vcgencmd measure_temp | measures CPU temperature
  
## Misc
  Directory | Description
  ------- | -----------
  date | Show current time and date
  ntpq -p | Show status of network time protocol. Used for syncing time from internet and GPS
  sudo halt | Shutdown
  sudo poweroff | Shutdown and turn off power (doesn't make a difference on a pi)
  sudo reboot | Reboots the system
  export PATH=$PATH:/home/me/myprogram | adds /home/me/myprogram to the PATH environment variable
  echo $PATH | shows the contents of the PATH environment variable
  env | shows all environment variables
  

## Redirects
  Directory | Description
  ------- | -----------
  (command) > (filename) | Sends the output from (command) to (filename)
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
      
   
      
  
 
