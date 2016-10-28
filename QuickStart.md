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

The project originated from [Gordon Williams](https://github.com/gfwilliams)
If you have an idea of what is a microcontroller but you never got the chance to program one, you should really spend some time reading the [Espruino Quick Start](http://www.espruino.com/Quick+Start).  

Espruino runs on microcontroller. Before going further in this guide you should have a look at the [supported hardware](http://www.espruino.com/Reference) and if you don't have any of those supported platforms, you may consider [buying one](http://www.espruino.com/Order#distributors).  
Basically, Espruino gives you the opportunity to deal with electronics using only Javascript. Really. How? Let me give you some examples:
- I'd like to turn on a LED: `digitalWrite(LED,1);`
- Or turn it off: `digitalWrite(LED,0);`
- I want to read a push-button: `digitalRead(BTN);`
- I want to play Counter-Strike on a microcontroller: Well, you don't. You prefer spend your time playing with TTN :-)

OK you got it. 
### IDE
You should have a look at the Espruino IDE doc [HERE](https://github.com/espruino/EspruinoWebIDE#espruino-web-ide--)
Historically this IDE was built (and is still) as a Chrome app. As Google announced [they will kill Chrome apps soon](http://venturebeat.com/2016/08/19/google-will-kill-chrome-apps-for-windows-mac-and-linux-in-early-2018/), Espruino IDE can now be built using Node.js (`npm install espruino-web-ide`).  
Last but not least, you even can use it as a real [web page](https://github.com/espruino/EspruinoWebIDE#full-web-version), but this only give you access to hardware through Bluetooth or Serial-over-audio-Jack.

The IDE is composed of 2 main parts. Left hand side is your console/serial port. Here you can read the output of your script that is running on Espruino board, and you can write any script live-time.  
Right hand side is your editor. Here you can write your application. Once you want to test it, just press the `Send to Espruino`(3) button.  
Talking about buttons (see following picture):
 1. Open a *.js file
 2. Save your script in a *.js file
 3. Send your script to Espruino
 4. Magic button. I let you discover it by yourself ;-)
 5. Connect/Disconnect your device. It is actually the Serial port manager
 6. Clear the console
 7. Settings. Click on the gear if you want to change Serial baudrate
<img src="https://raw.githubusercontent.com/yerpj/TTN_with_Espruino/master/images/IDE.png" width="1000">  

### Say Hello with Espruino
Once you have your Espruino device connected to USB/Serial and your IDE is started, just try to write this line 
```js
console.log("Thank you for reading this guide :-)");
```
Click the button (3), and you should read in the console something like that
```shell 
>reset();
=undefined
 _____                 _
|   __|___ ___ ___ _ _|_|___ ___
|   __|_ -| . |  _| | | |   | . |
|_____|___|  _|_| |___|_|_|_|___|
          |_| http://espruino.com
 1v87.840 Copyright 2016 G.Williams
>echo(0);
Thank you for reading this guide :-)
=undefined
> 
```
###Checking you have a version supporting [Promises](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Objets_globaux/Promise)
At the time of writing this guide, Promises are supported only from the [cutting-edge build](http://www.espruino.com/binaries/git/commits/master/). If your Espruino version is less than 1v88, you should upgrade your Espruino with version 1v87.xxx .   
For the Pico, here is latest the binary: [1vXX.YYY](http://www.espruino.com/binaries/git/commits/master/espruino_1v87.890_pico_1r3_wiznet.bin)  
If your Espruino version is 1v87 or above, you are just fine.
##  <img src="https://raw.githubusercontent.com/yerpj/TTN_with_Espruino/master/images/RN2483.png" width="100"> RN2483 module
The RN2483 module is a well known LoRa transceiver (mostly because it was the first certified module in EMEA). It embedds the LoRa stack, accessible trough a convenient serial port. I give you a few links, just in case you need it or by curiosity:
- [datasheet](ww1.microchip.com/downloads/en/DeviceDoc/50002346B.pdf)
- [Wiring up examples](https://www.thethingsnetwork.org/forum/t/how-to-build-your-first-ttn-node-arduino-rn2483/1574)
- [Wiring up for Espruino](https://github.com/espruino/EspruinoDocs/blob/master/devices/RN2483.md#wiring-up)  
You should follow the last link, as it has been written with love by [Gordon] and eventually you will need to know how to interface this module with Espruino, of course.
### make it accessible from Espruino
Once you spent some time wiring up, unplugging, correcting, inverting, soldering, wiring up once again your mess between RN2483 and Espruino, try to configure your serial port (in my case I am using pins `B6` and `B7`) at 57600 Baud.
```js
Serial1.setup(57600, { tx:B6, rx:B7 });
```
And create a RN2483 object:
```js
var RN2483 = require("RN2483");
```
Finally create your lora object:
If you already wired the RST pin of the RN2483 module, add it as the reset line (`B3`in my case). If not, don't care, it is not mandatory (at least for the purpose of this guide).
```js
var lora = new RN2483(Serial1, {reset:B3});
```
### Get your Device ID
Now, download your script into your device. If you are lost, just copy-paste this script and press the `Send to Espruino`button:
```js
var RN2483 = require("RN2483");
Serial1.setup(57600, { tx:B6, rx:B7 });
var lora = new RN2483(Serial1, {reset:B3});
```
Once done, try to write `lora.getStatus(function(x){console.log(x);})` in the console.
The parameter passed to getStatus() method is only a callback to print out the results of the function.
```shell
>lora.getStatus(function(x){console.log(x);})
=undefined
{
  "EUI": "0000000000ABCDEF",
  "VDD": 3.253,
  "appEUI": "0000000000000000",
  "devEUI": "0000000000ABCDEF",
  "band": "868",
  "dataRate": "5",
  "rxDelay1": "1000",
  "rxDelay2": "2000"
 }
> 
```
Fine, isn't it?
If you only want to get the devEUI without anything else, try with 
```lora.getStatus(function(x){console.log(x.devEUI);})```

## Configure your LoRaWAN and connect
[THIS SECTION SHOULD BE ADAPTED/CORRECTED BY SOMEONE SKILLED ON LoRaWAN CONFIG]
At this time you should already have a basic knowledge about [TTN](https://www.thethingsnetwork.org/). If not, so why are you still reading this guide :-) 
For the purpose, I consider that you already know what are the [Network Session Key and Application Session Key](https://www.thethingsnetwork.org/wiki/LoRaWAN/Security#security-in-lorawan-and-ttn). You should not know much about that, only that they come from the [TTN Dashboard](https://staging.thethingsnetwork.org/applications) whenever you create an application and register a device using the devEUI you just retrieved.  
Basically, just create 3 variables with the values given by your newly created application:
```
var devAddr="0000000000ABCDEF";
var nwkSKey="00112233445566778899AABBCCDDEEFF";
var appSKey="00112233445566778899AABBCCDDEEFF";
```
And simply call `lora.LoRaWAN`like this:
```
lora.LoRaWAN(devAddr,nwkSKey,appSKey,fun­ction(x){console.log(x);});
```
If you are covered by a TTN gateway, this function should return `OK`. 

## Send a message
BEFORE SENDING OR RECEIVING ANY MESSAGE, REMEMBER THAT THE LORA BANDWIDTH IS VERY LIMITED AND YOU SHOULD CONSIDER EVERY SINGLE BYTE EXCHANGED AS  BANDWIDTH-CONSUMING  

Now things go even easier. To send a message, just call `lora.LoraTX()`
```
lora.loraTX("Hello");
```

## Receive a message
