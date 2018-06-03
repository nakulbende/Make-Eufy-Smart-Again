# Make Eufy smart again!

Make a internet enabled IR controller for EUFY vacuum cleaners. Recent models of EUFY and Roomba vacuum cleaners include smartphone control, and my robot was feeling left out. So, lets make EUFY smart again!

## What you need: 

- EUFY vacuum cleaner: [non-internet enabled models v11, v11s and v11+](https://www.eufylife.com/collections/cleaning)
- ESP8266 based microcontroller: nodeMCU v0.9 used here, Adafruit Huzzah or any other internet enabled board can be used too
- Battery pack: Slimmer and bigger the better - current example uses a [12000 mAh battery charger](https://smile.amazon.com/gp/product/B077N9KYV8/ref=oh_aui_detailpage_o03_s00?ie=UTF8&psc=1)
- IR reciever: [VS1838B](https://smile.amazon.com/Haobase-pairs-Infrared-Emission-Receiver/dp/B01EMXC5XA/ref=sr_1_5?ie=UTF8&qid=1528055955&sr=8-5&keywords=ir+led+and+receiver) based. Wiring and further details [here](https://chioszrobots.com/2014/02/11/vs1838-tl1838-vs1838b-universal-infrared-receiving-head-remote-control/)
- IR LED: [950 nm](https://smile.amazon.com/Haobase-pairs-Infrared-Emission-Receiver/dp/B01EMXC5XA/ref=sr_1_5?ie=UTF8&qid=1528055955&sr=8-5&keywords=ir+led+and+receiver) Used like a regular LED
- Misc. supplies: Soldering supplies, wires, proto board, command strip (to mount controller, battery pack)

## Working principle: 

This project relies on using IR codes from the supplied remote meant for programming EUFY. The idea is to mount a low profile, internet enabled remote on the robot to make it fully controllable. This project includes the decoded codes for [Eufy v11](Codes_eufy_v11.txt). PLEASE PAY ATTENTION TO THE MODEL/  VERSION. You can re-learn the codes using the remote that came with your unit - as discussed shortly. 

For controlling, managing MQTTT web requests and GUI - we are going to usee the fantastic Blynk project. Using Blynk servers, we can also enable Google home/ Alexa support using IFTTT. 

Using a IR blaster controlled by esp8266, we can replay the codes as if they were coming from EUFY's original remote. 

Here is the step-by-step guide for copying IR codes > designing circuit > coding esp8266 > making Blynk GUI > integrating with IFTTT (and optionally with Google Home)

### Reading IR codes: 

All the IR send/ recieve commands are interfaced using cyborg5's amazing [IRLib2](https://github.com/cyborg5/IRLib2). Install it by suing library manager, or following instructions on the github page. Following instructions from the library's example [rawRecv](https://github.com/cyborg5/IRLib2/blob/master/IRLib2/examples/rawRecv/rawRecv.ino), I have included a cleaner version in this projet ([IR_read_RAW_codes](IR_read_RAW_codes/IR_read_RAW_codes.ino). To follow, simply connect the rightmost and center pin of IR reciever to 3.3V and GND pin of any arduino board, and the leftmost pin to digital pin 2.

Flash the board with included code, and open serial monitor with appropriat baud rate. Take your EUFY remote, point it at the reciever, and voila! The code will print the RAW IR code for that particular button. The EUFY's IR reciever is indeed following the exact same procedure to get signals from its remote!

![Circuit for copying IR codes](EUFY remote read_bb.png)

For the geeks and nerds out there, most consumer IR signals are carried on a 38kHz carrier frequency, which is true here. Many big brands like SONY, NEC and PANASONIC have HEX codes associated with this RAW data, and can be decoded using IRLib2. Since EUFY does not follow any of these codes - we will just read and send RAW IR codes - simply an array of numbers representing box wave (series of ON for certain amount of time, followed by OFF for certain amount of time). 
