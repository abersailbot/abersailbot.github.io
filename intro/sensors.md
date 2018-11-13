# Parts needed
 * Arduino
 * USB serial converter (TTL)
 * USB RS232 converter
 * GPS receiver (serial)
 * HMC6352 or 6343 compass
 * rotary wind sensor
 * ultrasonic wind sensor
 * 12V PSU
 * oscilliscope
 
 
# GPS

US satellite navigation system

medium earth orbit satellites

calculates time difference between you and each satellite

calculates 3D position (lat, lon, altitude) based on this.

accurate to around 5m in good conditions
altitude less accurate, around 10m

needs clear view of the sky and 4+ satellites
you should get around 10 on a good day outdoors

almanac (approx positions) and ephemeris data (more accurate) tell us which satellites to look for

EGNOS/WAAS geostationary satellites provide corrections based on ground error measurements, 15m down to 5m accuracy. Broadcast to whole continent.

DGPS sends local correction over VHF radio. Many recievers can't handle this. Can be done over internet or with own hardware.
Accurate to a few cm.

Dual/tri/quad mode Galilelo, Glonass and Baiedou receivers augment with GPS. 1m ish accuracy. Getting more common but not standard yet.

## Serial Ports

Sends data from a device to computer or other way round.

Connect PC's transmit line to device's recieve and vice-versa.

High voltage is a one, low voltage a zero.

Idle at high state. One bit low to start a byte. 7 or 8 data bytes. One bit high and back to idle to end it.

Typically 5V or 3.3V signals on microcontrollers.

Sometimes handshaking lines are uesd to show we've got data to send or are ready to recieve it. This is optional, often not used for things like GPS.

### RS232

(picture of an RS232 cable)

Heavier duty version of serial

Voltages negative and positive. Keeping average voltage at/near zero makes it less interference prone, better for longer distances.
Logic is inverted, negative means one and positive means zero!
Sometimes 0v is used instead of a negative voltage (cheap knock off hardware). Voltages anything from 5 to 12V.

A chip called a MAX232 will convert RS232 singals to 3.3V or 5V signals and invert them. 

## NMEA

North American Marine Electronics Association

NMEA0183 standard defines data used in boat electronics, like GPS receivers. 
Typically RS232 cabling, today its often behind a USB converter.

Data format 

Starts with a $

Two characters show which device is "talking".  GP means GPS, HC or HD compass/heading sensor, II wind sensor

Next 3 characters show what kind of data this is.

in GPS GGA gives position. VTG speed. RMC speed and position. Lots of overlapping sentences.

Then data comma seperated.

Finally a * and a checksum

No need to write your own code to read this. GPSD on Linux does it for you! Lots of Arduino libs too.

# Compass

## I2C

## Tilt compensation

# Wind sensors

## PWM

## Ultrasonic sensors
