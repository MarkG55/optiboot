## Optiboot Bootloader for Arduino and Atmel AVR ##

![http://optiboot.googlecode.com/files/optiboot.png](http://optiboot.googlecode.com/files/optiboot.png)

# Added changes to preserve most reset flags stored in MCUSR - only the Watchdog Reset flag is cleared. #

Even though the Watchdog Reset flag is cleared by the boot loader, user code can still detect a Watchdog Reset - if MCUSR is completely cleared, then the reset was due to the Watchdog!

Although the previous code stored the reset flags in r2, there was no way for the user code to distinguish between an external reset and a watchdog reset!  It also required extra code and an extra byte of RAM in the user sketch.

Additional changes made to allow user code to jump straight to the boot loader - boot loader will then wait a full 8 seconds before timing out and starting the user code.  This is useful in cases where a design has DTR disconnected from the reset pin, but still allows for firmware updates by triggering the bootloader in user code.

An additional advantage with these changes is that when uploading the boot loader to the chip with an In System Programmer, the boot loader will effectively run continuously afterwards until the board is either powered off, or firmware is uploaded to the chip - perfect for cases where DTR isn't connected to the reset pin!

Would be good to see my modified no wait mod included in the original Optiboot repository!



Optiboot is an easy to install upgrade to the Arduino bootloader within Arduino boards. It provides the following features:

  * Allows larger sketches. Optiboot is a quarter of the size of the default bootloader, freeing 1.5k of extra space.
  * Makes your sketches upload faster. Optiboot operates at higher baud rates and has streamlined programming.
  * Adaboot performance improvements. Optiboot runs your sketches sooner, with no watchdog issues.
  * Compatible with 168 and 328 Arduinos including Lilypad, Pro, Nano
  * Believed to work with ATmega1280 ("Mega"), ATmega644 ("Sanguino"), and ATmega1284 ("Mighty")
  * Supports several additional AVR chips (ATmega88, ATmega32)

Optiboot is now installed by default on the Arduino Uno. It can be installed on all older mega8, 168 or 328 based Arduinos.

## To install into the Arduino software ##
  1. Download the latest using Git or the Zip download feature of GutHub.  If you download as a zip, also extract it.
  1. You will need to be using a recent version of the [Arduino environment](http://arduino.cc), version 18 or later.
  1. Create a 'hardware' directory inside your sketches folder.
  1. Copy the optiboot directory into the hardware directory.
  1. Restart the Arduino software. New boards will appear in the Tools>Board menu.

## To burn Optiboot onto an Arduino board ##
  1. Select the appropriate Optiboot board type (or non-Optiboot if you want to change back)
  1. Connect your Arduino to an ISP programmer [[Installing]]
  1. Use the 'Burn Bootloader' item in Arduino.
  1. You can then upload sketches as normal, using the Optiboot board type.

----

> Although it has evolved considerably, Optiboot builds on the original work of Jason P. Kyle (stk500boot.c), [Arduino group (bootloader)](http://arduino.cc), [Spiff (1K bootloader)](http://spiffie.org/know/arduino_1k_bootloader/bootloader.shtml), [AVR-Libc group](http://nongnu.org/avr-libc) and [Ladyada (Adaboot)](http://www.ladyada.net/library/arduino/bootloader.html).

> _Optiboot is the work of Peter Knight (aka Cathedrow). Despite some misattributions, it is not sponsored or supported by any organisation or company including Tinker London, Tinker.it! and Arduino._  
> Maintenance of optiboot was taken over by Bill Westfield (aka WestfW) in 2011.
