arduino-tiny-841
============

A fork of shimniok's ( github.com/shimniok ) fork of arduino-tiny, which made an attempt to support the Tiny841. All work appears to have stopped on that core, and it was never in a state where sketches could be compiled (it looks like the initial work was never completed). 

This fork aims to finish what he started and add working support for the ATtiny841 on Arduino. 

Additionally, it brings in support for the ATTiny1634, brought in from rambo's 1.0.6 ATTiny1634 core. 

Status
===========

* Optiboot bootloader included, and works
* Includes board definitions + optiboot for 841 at 8mhz,  16mhz, and 20mhz (overclocked), and 1634 at 8mhz and 12mhz.
* Serial and Serial1 work. 
* INPUT_PULLUP works
* millis and micros work
* analogRead() works
* PWM works on all 6 channels (4 for 1634, naturally). 
* EEPROM works.
* tone is untested. 
* SPI works. 
* I2C/TWI hardware slave supported by WireS library: https://github.com/orangkucing/WireS
* I2C/TWI software master appears to work: https://github.com/todbot/SoftI2CMaster
* On the Tiny1634, there is a USI, which should work with the existing USI libraries to function as I2C master. 
* Pin change interrupts work.
* Some people have problems programming it with USBAsp and TinyISP. I used to, but today I tried, having changed nothing, and my USBAsp works just fine. Funky stuff. ArduinoAsISP works reliably (albeit slowly)
* Optiboot without the LED blink (noLED) for 841 included; this saves 64 bytes of flash (not used by default - modify boards.txt if needed)
* Board Manager support planned once the dust around that feature settles. 


Hardware
============

For use with Optiboot, the following components and connections are required:
* Arduino pin 9/PA1/TXD0 to RXI of serial adapter (0/PB0 on 1634)
* Arduino pin 8/PA2/RXD0 to TXO of serial adapter (1/PA7 on 1634)
* Diode between Reset and Vcc (band towards Vcc)
* 0.1uf capacitor between Reset and DTR of serial adapter
* 10k resistor between reset and Vcc
* (optional) LED and series resistor from Arduino pin 2/PB2/physical pin 5 to ground (This is the pin optiboot flashes)

An example amenable to home etching can be found at http://drazzy.com/e/boards/boards.php

Suitable breakout boards can be purchased from my Tindie shop:

841: https://www.tindie.com/products/DrAzzy/attiny84184-breakout/ 

1634: https://www.tindie.com/products/DrAzzy/attiny1634-breakout-wserial-header-bare-board/ (restock expected between 6/17 and 6/20/2015)

Installation
============

INSTALLATION

First ensure the Arduino software is correctly installed, and that the IDE is not running during the installation process. 


* Locate your Arduino Sketch folder.  This is the folder where the Arduino IDE
  stores Sketches, typically located in your Documents folder. 

* Ensure the "hardware" folder exists under the Arduino Sketch folder. If it is not there, create it. 

* Download Arduino-Tiny-841 from github as a ZIP file, and extract it into the 
  "hardware" folder, or simply clone the github repo into there.  For example,
  if the Arduino Sketch folder is...

      C:\Users\YourName\Documents\Arduino

  After extracting, the following files / folders should exist...

      C:\Users\YourName\Documents\Arduino\hardware\arduino-tiny-841\LICENSE
      C:\Users\YourName\Documents\Arduino\hardware\arduino-tiny-841\avrdude_conf16x.txt
      C:\Users\YourName\Documents\Arduino\hardware\arduino-tiny-841\avrdude_conf106.txt
      C:\Users\YourName\Documents\Arduino\hardware\arduino-tiny-841\avr\Boards106.txt
      C:\Users\YourName\Documents\Arduino\hardware\arduino-tiny-841\avr\Boards.txt
      C:\Users\YourName\Documents\Arduino\hardware\arduino-tiny-841\ChangeLog
      C:\Users\YourName\Documents\Arduino\hardware\arduino-tiny-841\README
      C:\Users\YourName\Documents\Arduino\hardware\arduino-tiny-841\README.md
      C:\Users\YourName\Documents\Arduino\hardware\arduino-tiny-841\avr\platform.txt
      C:\Users\YourName\Documents\Arduino\hardware\arduino-tiny-841\avr\programmers.txt
      C:\Users\YourName\Documents\Arduino\hardware\arduino-tiny-841\bootloaders\
      C:\Users\YourName\Documents\Arduino\hardware\arduino-tiny-841\avr\cores\

  The following folder should contain the source files for the Arduino-Tiny
  core...

      C:\Users\YourName\Documents\Arduino\hardware\arduino-tiny-841\avr\cores\

* Locate avrdude.conf - typically in 
  C:\Program Files (x86)\Arduino\tools\avr\etc 

* If you are using Windows Vista or later, right-click avrdude.conf and
  choose the Security tab. Select "Users", and see if there is a checkmark 
  in the "Allow" column for "Full Control". If not, click Edit, select Users, 
  and click the checkbox to Allow Full Control. Apply.

* Open avrdude.conf using any text editor. At the end of the file, copy+paste the contents of avrdude_conf_16x or 106 (depending on which version of the IDE you are using)

* If YOU ARE USING ARDUINO VERSION 1.6.2, delete platform.txt and rename platform_162.txt to platform.txt. 

* If you are using Arduino 1.0.x, move the contents of C:\Users\YourName\Documents\Arduino\hardware\arduino-tiny-841\avr\ to C:\Users\YourName\Documents\Arduino\hardware\arduino-tiny-841\ 

*IF YOU ARE USING ARDUINO 1.0.x, you must update the compiler toolchain* 
  
* Download and install Atmel Studio 6.2 (available from the Atmel website). 

* Locate the location of the Arduino toolchain, typically in:

  C:\Program Files (x86)\Arduino\tools\avr

* If using Windows Vista or later, right-click avr folder, Security tab. 
  Select "Users", and see if there is a checkmark in the "Allow" column for
  "Full Control". If not, click Edit, select Users, and click the checkbox
  to Allow Full Control. Apply.

* Copy the AVR toolchain from Atmel Studio over the old Arduino Toolchain, 
  replacing files when prompted. 

  C:\Program Files\Atmel\Atmel Toolchain\AVR8 GCC\Native\(version)\avr8-gnu-toolchain

  You must leave the old toolchain there, and copy these over it, because
  there are files needed by Arduino in addition to the toolchain that are
  located in the same directory. 
