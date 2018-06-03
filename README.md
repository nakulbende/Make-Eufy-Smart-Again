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

Here is the step-by-step guide to learn IR codes > make circuits > program esp8266 > develop Blynk project > integrate with IFTTT 

## Reading IR codes: 
