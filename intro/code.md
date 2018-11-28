# Boatd
![boatd arch](https://boatd.readthedocs.io/en/latest/_images/boatd-arch.png)

![kragniz](https://pbs.twimg.com/media/CkkXVe1XAAADCIk.jpg)

[boatd docs](https://boatd.readthedocs.io/en/latest/)

* Web API for boat information
 * Driver supplies: wind direction, waypoints, position, heading, sail/rudder positon. 
 * interface via http on port 2000
 * JSON formatted responses
 * curl http://localhost:2000/
 * /boat for position, heading and wind
 * /wind gets wind direction
 * /waypoints gets waypoints list, can also send a waypoint list
 * /behaviours shows which behaviours are loaded/running
 
## Drivers
  * Interface to hardware or simulator
  * Driver can be changed via config
  
### [Dewi-boatd-driver](https://github.com/abersailbot/dewi-boatd-driver/blob/master/dewi_boatd_driver.py)
 * Interfaces Dewi's hardware to Boatd
 * Sends command to the arduino
 * Reads GPS via gpsd
 * Simple protocol to arduino, 'c' = get compass, 'w' = get wind, 'r' = set rudder, 's' = set sail
 
#### [dewi-arduino](https://github.com/abersailbot/dewi-arduino/blob/master/src/dewi.ino)
  * Only bit not in Python, only 180 lines
  * Listens for c,w,r and s commands. Expects r/s to be followed by a number. 
  * Responses from c/w are wrapped in JSON notation
  
## Plugins
  * Extends boatd functionality
  * Plugins for logging and mavlink telemetry
 
## Configuration
 * [example config](https://github.com/boatd/boatd/blob/master/boatd-config.yaml.example)
 * YAML file
 * defines waypoints file, boatd port, plugins, drivers, behaviours
### Waypoints file
 
  
## Other boatd utils
### [boatd-opencpn](https://github.com/boatd/boatd-opencpn)
  * Sends NMEA GPS, compass, wind and rudder position strings to the openCPN chart plotter.
  * Bug in rudder position
  * Requires a web connection to boatd, only works over wifi right now.
  
### [cboatd](https://github.com/boatd/cboatd)
  * simple console output of boatd's state

# Boatdclient
* Python client for binding to boatd's web interface. 

# [Dewi-behaviour](https://github.com/abersailbot/dewi-behaviour)
## navigate.py
* Main control system file, common to all behaviours
* Navigator object
### __init__  function
* initalises variables
### update function
 * Main control logic
#### Tacking Logic
#### Rudder setting 
##### PI controller
* Three point/bang bang control
* Rudder controls heading, aim is to keep difference between heading and error at or near zero.
* Rudder left,centre or right. Centered whenever within some deadband, maybe 20 degrees.
* Propotional control, move rudder in proportion to heading error. "gain" value is what we multiply heading error by to get rudder position.
* Get gain too big and it will oscilate. Too small and it won't converge. 
* Tends to cause a small constant error offset (steady state error).
* Integral control, take the sum of errors over time. Integral gain is usually tiny. Multiply integral error sum by gain and add to output of p controller.
* Will correct steady error. If something stops us turning for a while integral error builds up, when we do turn it can over power the system.
* Solution is to gradually decay the integral error,multiply by 0.99 each time round the loop.
* Derivative control looks at rate of change in the error, we don't use it.
* https://www.youtube.com/watch?v=fusr9eTceEo
##### cross track minimisation
* Measure distance between line from A to B and our current position.
* Correct by turning back towards the line.
* Without it we tend to get arcs, not lines between points. 
![cross track error](https://static.rcgroups.net/forums/attachments/1/7/0/7/2/a1992926-93-Heading%20and%20Bearing%20-%20Copy.jpg)
#### Sail setting 
* Calls choose_sail_angle function
* Figures out sail angle based on wind direction
* mapping function of wind angle to sail angle

### Run function
  * Main loop
  * Gets the target heading to the waypoint
  * runs update
  * logs timing info for debugging
  
## Behaviours

### [virtual-anchoring-behaviour](https://github.com/abersailbot/dewi-behaviour/blob/master/virtual-anchoring-behaviour)
* Just sails to a point and keeps trying to hit it
* Broken!

### [area-scanning-behaviour](https://github.com/abersailbot/dewi-behaviour/blob/master/area-scanning-behaviour)
* sail to all squares in a grid
* broken?

### [waypoint-behaviour](https://github.com/abersailbot/dewi-behaviour/blob/master/waypoint-behaviour)
* Main behaviour
* follows a list of waypoints loaded from a file

### [looped-waypoints-behaviour](https://github.com/abersailbot/dewi-behaviour/blob/master/looped-waypoint-behaviour)
* like waypoint behaviour but goes back to first waypoint at the end

### [station-keeping-behaviour](https://github.com/abersailbot/dewi-behaviour/blob/master/station-keeping-behaviour)
* Tries to stay in a box for 5 minutes exactly
* sails to centre and then leaves 

# Simulator
* [Sailsd](https://github.com/sails-simulator/sailsd), also by Louis Taylor (kragniz)
* [libsailing](https://github.com/sails-simulator/libsailing) provides physics model to sailsd.
* Interfaces to boatd with its own driver
* Sails runs its own protocol for communitcating internally between its server and GUI (sails-ui). GUI only for output, doesn't need to run.
* slightly modified [behaviour](https://github.com/abersailbot/simulator-behaviour) based on dewi's behaviours. Different tacking angles, rudder gains and sail angles.


