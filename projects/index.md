---
layout: default
title: Wicked Rainman's projects
---

# Programming projects 
---------------------
__DAPL__     

Spent quite a while writing the _Data Analist Programming Language_. It's supposed to make life a bit easier when your looking for interesting patterns of activity in things like Web logs Etc. The whole idea seems to have fallen on deaf ears (maybe because it's no good), but I've left the code around just in case anyone shows any interest. Have a look [here](https://github.com/wicked-rainman/DAPL "Go on, click it. You know you want to!") if you are interested.   

------------

__Micro dot pHAT for a Raspberry Pi__

![](/pictures/phat1.png "It's upside down so the Raspberry pi can sit flat")

Recently bought a Micro Dot pHAT to go on a Raspberry Pi. Onboard are three smt IS31FL3730 chips and three pairs of matrix displays all driven over I2C.  It comes as a kit so you have to solder on the GPIO connector and all the DIL led display chips (The IS31FL3730 have already been installed) which took me about half an hour.  

I couldn't find  any C programs to get the board going (everyone seems to love python these days!) In the end I grabbed fragments of code I found on the Internet and wrote a small set of [functions](https://github.com/wicked-rainman/Rpi-Micro-Dot-pHAT "Print a string, update and reset the display and set brightness") that I think are useful. Help yourself if you were looking for a simple solution.

-------------------

__Indoor display for Aercus IP weather station__

A few years ago I purchased an [Aercus}(http://www.aercusinstruments.com/aercus-instruments-weathersleuth-professional-ip-weather-station-with-direct-real-time-internet-monitoring/) weather station. and configured it to send all the data to Weather Underground.

