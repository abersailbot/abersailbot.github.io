# Introduction to electronics and soldering

## Soldering

### Safety 

 * Don't breathe in solder smoke
 * Wash your hands after using solder. Especially if its leaded solder. Don't touch your lips. 
 * Only hold the handle of the soldering iron.
 * DON'T do this:
 
 ![Don't do this!](https://i2.wp.com/makezine.com/wp-content/uploads/2016/03/Screen-Shot-2016-03-08-at-9.15.01-AM.png)
 
 
### How to solder
 * Let the iron heat up, it will smoke a little when its hot
 * Heat the track of the circuit board and the thing you want to solder
 * Feed in solder between the iron, track and item you're soldering
  ![It should looke like this](https://cdn.sparkfun.com/r/600-600/assets/learn_tutorials/5/Soldering_Action-01.jpg)
  * A blob will appear around the leg of the component you're soldering
  * Be careful not to join solder onto neigbhouring pins/tracks.
 
## Wiring Conventions
 
* Red is positive, often 5V
* Black is negative
* Where 12V and 5V are used, 12V is often yellow

 
## Electronic components
 
### Resistors
  
  Resistors limit the amount of electrical current which can flow. They are measured in units called ohms (represented by a Ω symbol). The more ohms the less current will flow. When drawn in circuit diagrams they use this symbol:
  
![resistor symbol, a line which goes up and down with 45 degree slopes a few times](https://upload.wikimedia.org/wikipedia/commons/thumb/e/ee/Resistor_symbol_America.svg/320px-Resistor_symbol_America.svg.png)

Sometimes this symbol is used instead:

![IEC resistor symbol, a long rectangle](https://upload.wikimedia.org/wikipedia/commons/thumb/c/c3/Resistor_symbol_IEC.svg/320px-Resistor_symbol_IEC.svg.png)
  
#### Ohm's Law
  
  ```V = I * R```
  
  V voltage (volts)
  
  I current (amps)
  
  R resistance (ohms)
  
#### Resistor colour codes 
  
  Resistors use a colour code to show their value. 
  ![Resistor colour codes](https://www.digikey.co.uk/-/media/Images/Marketing/Resources/Calculators/resistor-color-chart.png?la=en-GB&ts=e802ab48-1ea0-4745-babf-9a21accec5c2)
  
  Alternatively we can use a multimeter in resistance mode (often the Ω symbol) to measure a resistor. Some meters might require us to choose a resistor range, we might have to jump through these to get a reading.
  
[Find out more about resistors](https://learn.sparkfun.com/tutorials/resistors/decoding-resistor-markings)
 
### Diodes

Diodes only let electricity flow one way through them. In circuit diagrams they are drawn using this symbol:

![Symbol for a diode](https://cdn.sparkfun.com/assets/d/6/b/f/a/5171b6bece395ff53c000000.PNG)
 
They usually have a white or silver line across them marking the negative side. Diodes can be used to protect a circuit against power being connected the wrong way. Voltage across a diode drops by 0.6 to 1V, this is called forward voltage.

[Find out more](https://learn.sparkfun.com/tutorials/diodes/all)
  
### LEDs
 LEDs are diodes which emit light. They are a nice low power solution for lighting. 
 
 They are represented by this symbol:
 
 ![Symbol for an LED](https://upload.wikimedia.org/wikipedia/commons/thumb/e/e5/LED_symbol.svg/320px-LED_symbol.svg.png)
 
 The positive side (anode) should have a longer leg. The negative side (cathode) is shorter and the edge of the plastic cover is flat. We need to limit the amount of current going through an LED. We do this with a resistor, without it the LED will get hot and eventually burn out, but it will work for a short time. The resistor should be placed between the negative side of the LED and the negative side of the battery or power supply. The circuit should look like this:
 
 ![Example LED circuit](https://upload.wikimedia.org/wikipedia/commons/thumb/c/c9/LED_circuit.svg/240px-LED_circuit.svg.png)
 
To find out what resistor to use we can guess, 330 ohm is typically a good value. Get the resistance too high and the LED will dim. Get it too low and it will get hot. Alternatively we can calculate it, but this needs a few parameters from the LEDs datasheet. If we don't have these we can guess with typical values. Use the calculator at https://www.kitronik.co.uk/blog/led-resistor-value-calculator/ to work this out. 
 
[Find out more](https://learn.sparkfun.com/tutorials/light-emitting-diodes-leds)
 

 
### Capacitors
 Capactiors store a small amount of electrical current. They are often used to smooth out unstable power supplies or to stop voltage drops when a heavy duty device (e.g. a motor) switches on. 
 
 The symbol for a capacitor is ![capacitor symbol](https://upload.wikimedia.org/wikipedia/commons/8/89/Capacitor_Symbol.svg).
 
 Capactiance is measured in farads. A farad is quite a lot, most capacitors are pico (millionths) or micro (thousanths) of a fard. A one farad capacitor can store one coulomb of charge at one volt. One amp is equal to one coulomb per second. So a one farad capacitor, holds one amp-second at one volt. 
 
 There are lots of types of capacitors, the most common are ceramic capacitors which look like a round disc and are typically a dull yellow colour or electrolytic capacitors which look like a cylinder. 
 
 A ceramic capacitor ![ceramic capacitor](https://media.rs-online.com/t_large/R5381310-01.jpg)
 
 An electrolytic capacitor ![electrolytic capacitor](https://media.rs-online.com/t_large/F3654650-01.jpg).
 
 The polarity of an electrolytic capacitor matters! It has a big minus symbol on the negative side. The negative side is typically shorter. 
 
 [Find out more](https://learn.sparkfun.com/tutorials/capacitors)
 
### Power, Voltage and Current
 
 * Current measured in amps, which are the number of electrons flowing through the circuit.
 * Volts measure the size of the force sending the electrons through the circuit.
 * Watts measure the amount of power being used (or generated) at an instant in time.
 
 ```watts = volts * amps```
 
#### Energy and batteries
 
 * Battery capacities are usually in watt hours. Domestic electricity is usually billed in killowatt hours.
 * One watt hour = supplying one watt for one hour
 * Sometimes written in amp hours (or milliamp hours) instead, a 12V 1AH battery is a 12 Watt Hour battery. 
 * Can also be measured in joules, one joule = one watt second, 3600 joules = one watt hour. 

 [Find out more](https://learn.sparkfun.com/tutorials/electric-power)
