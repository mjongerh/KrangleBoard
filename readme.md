# Krangle keyboard, a keyboard with way too many buttons
Originally I wanted a keyboard with some additional keys for the purpose of shortcuts in games. 
Then I got inspired by the SpaceCadet and the hyper7 and wanted more buttons, for shortcuts, macros and snippets in coding. 
Unfortunately I couldn't get a keyboard that would suffice my greed, so instead I made my own!
With no experience in building keyboards or 3D-modeling or 3D-printing, I thought I would be a perfect fit for this project.

A lot of insipration was taken from [this](https://github.com/jurassic73/split89/blob/main/readme.md#prepping-the-diodes) example.
It contains a great description of many steps of the assembly process.
I highly recommend to read through it if one intends to builds this or any other 3D-printed handwired keyboard.

A little soundtest for the nerds: https://youtu.be/8HYNmcfg844

## Layout
For the layout I went with a lot of extra buttons for programming and gaming.
Further explaination and information in the [layout](./Layout) section

## Hardware
### 3D modeling the case
In the [STL files](./STLfiles) one can find the stl files for all the parts used.
It was intended to be printed on a creality CR-20, hence the maximum size is 220mmx220mm.
It is definitely not perfect as it was made in SketchUp by a noob.
I would not recommend to us it as a template, but it works as-is and might be helpful as inspiration.
Potential improvements are discussed in the [STL](./STLfiles) section.


### Wiring
Initially the plan was to use 2 microcontrollers, considering the amount of buttons.
However, this has proven to be more difficult than expected.
So instead, I was able to fish a teensy2.0++ from the past and wired everything on a single controller.
In this case it uses the traditional method for wire mapping. (PIN map found in [software](./Software))
Some of the macro wiring does not make sense in this setup, but it was a leftover from a previous attempt.
Considering the amount of space in the keyboard, it should be fine for anyone.
![image](https://github.com/mjongerh/KrangleBoard/blob/master/Images/wiring.png)

Many great tips and tricks can be found externally, for example in [this](https://github.com/jurassic73/split89/blob/main/readme.md#prepping-the-diodes) repo of another 3D printed board.
Out of enthousiasm I designed and 3D-printed a little tool to be used as guidance to bend the pins of the diodes.

### LED circuitry
As the power output of the PINS on any microcontroller are very limited, I used a seperate 5V source for the main set of LEDs.
I cut of one ends of a USB cable and stripped the internal wires.
Only the red(+) and black(-) ones a relevant, so the data wires can be cut off as well.

A typical mothed would be to solder a resistor to each LED and then connect them in parrallel.
This would enable to control each LED individually, which is not on my list of desires and would complicate the connections with the (additional) microcontroller.
However, I am not aware of another benefit of this, apart from a potential short-circuit if one LED somehow breaks.
So I choose to connect all LEDs in parallel with a resistor in series to limit the current.
All negative poles can be soldered in a row and the positive poles likewise.

By connecting these rows together, one ends up with a single point that acts a connection for the negative poles of all LEDs and one for the positive poles.
To control the current to an appropriate level I used ohms law (R=U/I) to calculate a required resistance.
With a maximum of 2mA per LED (obtained experimentally), this would lead to a load resistor of ~15Ω.

To control the current (and therefore the brightness) through the LEDs, I used a MOSFET as 'electronic switch'.
Additionally, two resistors are required as pull-up and pull-down resistor to stabalize the voltage.
This image shows an example setup for the circuit.
Where G,D ans S and the Gate Drain and Source pins of the MOSFET.
PIN indicates the connection to the controlling pin of microcontroller. (PIN map found in [software](./Software))
![image](https://github.com/mjongerh/KrangleBoard/blob/master/Images/MOSFET.png)

The MOSFET and resistors are placed on the bracket, there is intentionally left some space for this.

The indicator LEDs can be connected directly to the microcontroller, since a single LED don't draw too much current.
This means that a load resistor (2500Ω) should be placed between the microcontroller and the positive end of the LED.
The negative pole of the LED can be connected to the great negative row of the main set of LEDs.
Alternatively it can be connected to the ground pin on the microcontroller.


## Assembly
This section will just show some of the progression of my build.
As a bonus, one will notice how this keyboard got its name.

After putting all the main switchplates and case parts together and pressing all switches in place.
![image](https://github.com/mjongerh/KrangleBoard/blob/master/Images/part1.jpg)
![image](https://github.com/mjongerh/KrangleBoard/blob/master/Images/part2.jpg)

Closeup of the wiring and my lackluster soldering skills. 
The bare wires are the pins of the diodes and function as the rows.
The colored wires connect the other pins of the switches and make up the columns.
White and black wires are the + and - of the LEDs.
![image](https://github.com/mjongerh/KrangleBoard/blob/master/Images/closeup.jpg)
![image](https://github.com/mjongerh/KrangleBoard/blob/master/Images/closeup2.jpg)

After connecting the LEDs and testing them.
![image](https://github.com/mjongerh/KrangleBoard/blob/master/Images/part3.jpg)

Closeup of how the MOSFET is installed
![image](https://github.com/mjongerh/KrangleBoard/blob/master/Images/mosfetinstall.jpg)

The beauty in all its glory.
On a daily basis I pray for the wires or one of the connection not to break.
![image](https://github.com/mjongerh/KrangleBoard/blob/master/Images/part4.jpg)
![image](https://github.com/mjongerh/KrangleBoard/blob/master/Images/desk.jpg)

