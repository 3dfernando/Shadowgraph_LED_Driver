# Shadowgraph LED Driver
A simple electronic circuit board design for overdriving a pulsed LED flash for shadowgraph purposes. 

*** WARNING: This circuit overdrives an LED with up to 200A of current. COMPONENTS WILL GET BURNED! Be careful in your explorations and make sure you understand the circuit before you start messing with it! ***

# Circuit Description
The circuit schematic, provided in Circuit Diagram.pdf, is very simple. 
24V are provided to a nominally 3.8V LED through a high-power MOSFET (IRF3805) for the duration of the input pulse, which should be very short (order 10us or less) and of very low duty cycle (less than 1% recommended).

The current provided to the LED can reach 200A at full power. 200A will, however, explode the LED bond wires, rendering it useless. Since the LED is very expensive (about $100 as of 2023 for the white LED), it is not recommended to drive at max power. The LED provides a good flash at 100-120A and you should really not exceed 150A (that's where sometimes it may or may not burn depending on other conditions).

There is so much current in such a little time to run the LED that the MOSFET IRF3805 needs a driver IC to provide the inrush current of up to 8A. This obviously cannot be provided by a function generator, which is why the UCC27424 is there to convert the high impedance of the fn. generator to a low impedance required by the MOSFET gate. The UCC27424 can be destroyed if the MOSFET fails. This is because when the MOSFET fails, it can fail such that the Gate and Source terminal are shorted. In this case, the current going through the UCC driver will exceed the 8A rating and burn the IC, so both need to be replaced in this case.

To adjust the amount of current going through the LED, adjust the output voltage of the LM2596 DC-DC converter circuit. This can be done using a small screwdriver to adjust the trimmer-potentiometer in the DC-DC converter. The output voltage will range between 9 and 16V during operation, depending on the amount of current you want for the LED. 

The amount of current running through the LED can be measured with an oscilloscope by watching the voltage drop across the 0.02Ohm resistor. For 100A, for example, we have V=I*R=100A * 0.02Ohm = 2V across the resistor. Since the LED is expensive, you can connect a piece of short wire between the LED terminal connectors (i.e., generate a short circuit), in order to test the system. Once you are confident the current is about 100A or so, connect the LED and test your optics to see if the brightness is sufficient. If it isn't, you can increase the power by using the trimmer-potentiometer in the DC-DC converter, bearing in mind that at about 150A the LED, MOSFET and UCC driver will be destroyed.


Note: The LED has a small thermal mass and will heat up rather quickly if you use a high duty cycle for this driver. The average power dissipation of the LED can exceed 1200W with 1% duty cycle, meaning you will not be able to build a heat sink with acceptable specs for the LED. Best is to simply bolt the LED to a large aluminium block to provide it with thermal mass, and just not run it for too long. The LED may fail over a few minutes if it overheats.

# How to make this
1. First, download Gerbers.zip and send the Gerber files to a PCB manufacturer company.
2. Assemble the PCB according to Circuit Diagram.pdf. Make sure all components are oriented correctly! The bill of materials is provided in BOM.xlsx
3. There is an Operation Instructions.pptx file with directions and pictures on how the PCB looks like. The terminal blocks and DIP8 socket enable replacement of the components that are likely to be damaged if you don't know what you are doing. Make sure you buy extra transistors IRF3805 and UCC27424P chips, as they really can burn very easily until you understand the limitations of this device. 
4. Start testing the board, according to the instructions and warnings in "Circuit Description". Have spare parts - you will need them!

# Known operation conditions
This circuit has been successfully operated at conditions listed below:
* 500Hz, 10us pulse width, indefinitely;
* 500kHz, 0.5us pulse width, for 2-3 seconds (Pulse burst mode in a function generator);
* 10-50kHz, 1us pulse width, for ~30 seconds;
* Minimum pulse width to get any meaningful amount of light is about 100ns (See Pictures/Photodiode measurements folder);
* This circuit is not designed to operate without pulsing (i.e., continuously). Likely all components will fail due to the extremely high currents.


As you can see, this is a very tricky circuit to work with. It provides some real juice for your shadowgraphs, allowing for imaging at very high frame rates. Have fun building it!
