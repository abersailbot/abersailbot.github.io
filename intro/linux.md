# Introduction to Linux for Robotic Sailing

## Logging in

## Filesystem commands
mount
df -h
du -h <directory>


## Processes

ps aux
ps -u <username>

## File transfer
scp filename username@hostname:<remote dir name>
scp filename username@hostname:
scp username@hostname:<remote dir name> filename


## Networking

curl
wget
ifconfig
ip route show

## Packaging

dpkg -l
dpkg -L <packagename>
apt search <packagename> or apt-cache search <packagename> 
sudo apt install <packagename> or apt-get install <packagename>
sudo apt update
sudo apt upgrade

## User management

sudo adduser <username>
groups <username>
sudo usermod -aG <groupname(s)> <username>

## Hardware

dmesg
lsusb
lsblk
lscpu
free
cat /proc/meminfo
cat /proc/cpuinfo


## Misc
date
ntpq -p

## Redirects

## Pipes


