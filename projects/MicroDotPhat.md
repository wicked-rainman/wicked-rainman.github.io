# Micro dot pHAT for a Raspberry Pi

![](/pictures/phat1.png "It's upside down so the Raspberry pi can sit flat. I've coded the fonts so they are up-side down too.")

Recently bought a Micro Dot pHAT to go on a Raspberry Pi. Onboard are three smt 
[_IS31FL3730_](http://ams.issi.com/WW/pdf/IS31FL3730.pdf "PDF - Audio modulated Matrix LED driver") chips and three pairs 
of [_matrix displays_](https://shop.pimoroni.com/products/led-module-pair?variant=25455044487 "LTP-305 - They do other colours") all 
driven over I2C.  It comes as a kit so you have to solder on the GPIO connector and all the DIL displays (The IS31FL3730 have already 
been installed). This took me about half an hour.  

I couldn't find  any C programs to get the board going (everyone seems to love python these days!) In the end I grabbed fragments of 
code I found on the Internet and wrote a small set of C [functions](https://github.com/wicked-rainman/Rpi-Micro-Dot-pHAT "Print a 
string, update and reset the display and set brightness using the chip's PWM and Current registers") that I think are useful. Help 
yourself if you were looking for a simple solution.

In the repository you will find the following:

reset(int f_discriptor) : Resets the display and puts it back into default mode.

update(int f_discriptor) : Updates the display with any characters that have been sent

bright(int f_discriptor, int display_current, int display_pwm) : Sets the LED brightness of the display

printstr(int f_discriptor, char string) : Sends a string to the display for printing

printchar(int f_discriptor, int position, int char) : Sends a character to one of the 6 matrix displays
