<H1 align="center">M5Station as a portable weather and environment monitor</H1>
<p align="center">
<img width="800" height="677" src="/pictures/PXL_20221213_091805288.jpg">
 </p>

I spend many a happy hour looking out the windows as the clouds pass by. To enhance this enjoyment I've built a portable weather station. 
It's all pointless because I never go anywhere, but that's besides the point.

## My objectives were:

+ To make up an excuse to buy an M5Station-bat (because they look cool and have built in batteries that will give a long run time.
+ To see if I could hack together a string of sensors all attached to one I2C port
+ To have a go at moving from the Arduino IDE to Visual Studio Code and Platformio. 
+ Make something with a minimal AP interface.
+ Design and print a cool case that makes it look like something more expensive.

As far as projects go, I think I met all the objectives except the last one. My 3D printer has given up the ghost, which is why all the sensors 
are stuffed into a crappy box. At that stage I lost all interest in the project, yet I'm still typing.

## Implementation
+ The first issue I wanted to solve was with the GPS. I'm using one of the cheap M5Stack GPS/BDS modules. The problem is, it outputs data slowly on a
serial port. I therefore had to find a serial to I2c solution. In the end I found Gravity do an I2C to dual UART module that looked like it would
do the trick. It seems to work fine, although I did note the odd GPS sentence being truncated. I don't know if that's a fault in my code or something to
do with the onboard circular buffer size, but it's not proved to be a major issue.

+ The second issue is one of record storage. There's no built in SD card reader in the M5Station and as I've said earlier, I wanted to have one single
I2C string (Most, if not all SD readers are SPI). I opted for a 32KB Fram board. That's not much in the way of storage, but I've found that writing 
100 byte string records gives about 15 mins of recording time. I could extend the time frame by reducing the frequency of writes,or by adding a
second board but I've not bothered.

+ All the other sensors (TVOC/eCO2, Lux, Temperature and pressure) just plug in to the string with no fuss. That just left some timing issues.
I use the GPS to set the RTC, so I have to wait around reading serial data until I come across the sentence I'm after, then do the RTC update. I also need
to read all the other sensors (which takes some time),keep a lock on my current GPS position and update the battery status. In the end, I solved this issue by writing a time-slice dispatcher class that will only allow each function to continue for an alloted time. It seems to work quite well..

+ I had to use a couple of I2C multi-gang hub boards. There are 5 I2C devices to string together. Disappointingly I could only
get hold of hub boards with 4 sockets (there are versions with 6, but couldn't source any), so with the uplink to the ESP board and a jumper to
connect each hub I used all the slots anyway.

## Code

+ The Dispatcher code can be found [here](https://github.com/wicked-rainman/ESP32Dispatcher). I'm sure I'll use it again on other projects so I think it was worth the effor
+ The MyStation code is [here](https://github.com/wicked-rainman/PortableWeatherStation). 

<p align="center">
<img width="600" height="800" src="/pictures/PXL_20221213_091716852.jpg">
 </p>
