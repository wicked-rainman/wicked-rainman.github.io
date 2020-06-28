__Indoor display for Aercus IP weather station__

A few years ago I purchased an 
[_Aercus_](http://www.aercusinstruments.com/aercus-instruments-weathersleuth-professional-ip-weather-station-with-direct-real-time-internet-monitoring/ "God 
bless the Aercus folks in New Zealand, but you can buy them in the UK from www.greenfrogscientific.co.uk" ) weather station and 
configured it to send all the data to [_Weather Underground_](https://www.wunderground.com/). My only complaint about this devices 
is it doesn't come with an indoor display.  

You can view the weather by directly connecting to the device's HTTP port, but I wanted something I could glance at without 
firing up a PC. To solve this I used a Raspberry Pi with a 
[_Micro dot pHAT_](https://shop.pimoroni.com/products/microdot-phat?variant=25454635591 "Go Sheffield!!!" ) attached and wrote 
a bit of [_code_](https://github.com/wicked-rainman/Aercus-IP-weather-station) that connects over WiFi and scrapes the local web 
page directly off the bridge/receiver. 

The code runs in a loop forever, so you either need to background it as a process or write a daemon so it runs from boot. 
I've not got a Raspberry Pi zero W yet, but that's my end target platform.  
