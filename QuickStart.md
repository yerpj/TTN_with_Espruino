# Quickstart 

## Introduction
This Quickstart guide is meant to give you a basic knowledge on how to use Espruino to send/receive message to/from The Things Network.  
If you want to learn Espruino, you should rather go [HERE](www.espruino.com).  
If you want to learn Javascript, you should rather try to ask [Google instead](https://www.google.ch/?gws_rd=ssl#q=javascript+basics).  
If you don't know what is The Things Network (TTN), please have a look at its wonderful dedicated [website](https://www.thethingsnetwork.org/)  
Throughout this guide, I will try to introduce you to Espruino, a LoRa module called RN2483, and finally I will show you how to exchange data with the TTN infrastructure. With some basic Javascript knowledge, you should be able to send a "Hello World" message to your TTN dashboard in about 15 minutes (considering you already have the required hardware).  
Talking about hardware... You should :
- [x] own an Espruino board. A [Pico](http://www.espruino.com/Pico) is perfect
- [x] have a RN2483 module mounted on a commercial breadboard (the one from Drazzy [on Tindie](https://www.tindie.com/products/DrAzzy/rn2483-breakout-bare-board/) for example). If you have a solder iron, you can try to do it yourself <img src="https://raw.githubusercontent.com/yerpj/TTN_with_Espruino/master/images/DIYBreadboard.jpg" width="80">
- [x] Be in the range of a TTN Gateway. If you don't know, this map can help you: [TTN gateway map](https://www.thethingsnetwork.org/map)
- [x] know what '3V3', 'GND', 'pin 17',..., means.

Your are OK with this list? Fine! GO on!


##  ![alt text](http://www.espruino.com/images/logo.png "Espruino logo")Espruino?
>Espruino is a JavaScript interpreter for microcontrollers. It is designed for devices with as little as 128kB Flash and 8kB >RAM.

If you have an idea of what is a microcontroller but you never got the chance to program one, you should really spend some time reading the [Espruino Quick Start](http://www.espruino.com/Quick+Start).  

Espruino runs on microcontroller. Before going further in this guide you should have a look at the [supported hardware](http://www.espruino.com/Reference) and if you don't have any of those supported platforms, you may consider [buying one](http://www.espruino.com/Order#distributors).  
Basically, Espruino gives you the opportunity to deal with electronics using only Javascript. Really. How? Let me give you some examples:
- I'd like to turn on a LED: `digitalWrite(LED,1);`
- Or turn it off: `digitalWrite(LED,0);`
- I want to read a push-button: `digitalRead(BTN);`
- I want to play Counter-Strike on a microcontroller: Well, you don't. You prefer spend your time playing with TTN :-)

OK you got it. 
### IDE
You should have a look at the Espruino doc [HERE](https://github.com/espruino/EspruinoWebIDE#espruino-web-ide--)
Historically this IDE was built as a Chrome app. As Google announced [they will kill Chrome apps soon](http://venturebeat.com/2016/08/19/google-will-kill-chrome-apps-for-windows-mac-and-linux-in-early-2018/), Espruino IDE can now be built using Node.js (`npm install espruino-web-ide`).  
Last but not least, you even can use it as a real [web page](https://github.com/espruino/EspruinoWebIDE#full-web-version), but this only give you access to hardware through Bluetooth or Serial-over-audio-Jack.

### Say Hello with Espruino
## RN2483 module
### Get your Device ID
## Configure your LoRaWAN
## Connect to TTN
### ABP method
### OTAA method
## Send a message
## Receive a message
