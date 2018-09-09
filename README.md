# Magic-Mirror
WiC Projects Committee 2017-2018 Project.

## Introduction
This year's project is a magic mirror or smart mirror. It functions as a mirror as it has a reflective surface but also includes helpful information as you get ready for your day. As for the technical setup of how it works, the basic setup includes a monitor powered by a raspberry pi with the [Magic Mirror](https://magicmirror.builders/) software installed on it. The software puts a full screen window of white text on a black background on the display so when a one way mirror is place over it, the white text shines through. Usually this mirror is actually acrylic where one side is see through and the other side is a reflective surface. The open source Magic Mirror software we used has built in and open source third party modules that do different things like show the weather, WiC's calendar, as well as the time and date. We also added sensors to the project which include voice command, audio response, a distance sensor, and a gesture sensor. These sensors interact with the modules or other code included on the pi.

## Hardware
This is a complete list of parts we used to create this project.

- Monitor: We used the Sceptre E series E205W 20" monitor. This model has the HDMI/VGA ports on the back but not along the side of the monitor making it easier to put in the frame and hook up to the pi. You can get this off of [amazon](https://www.amazon.com/Sceptre-E205W-1600-V1-LED-Lit-Monitor/dp/B00S8W8QMG/ref=as_li_ss_tl?ie=UTF8&qid=1473453637&sr=8-11&keywords=led%2Bmonitor&linkCode=sl1&tag=gjhug1-20&linkId=682d1cdafd514bdc5d7574a53848e341&th=1) or elsewhere. Note that if you change the monitor you will have to change the a lot of the other materials accordingly, as much of the measurements are based on that shape and size.
- Acrylic one way mirror. One side is reflective and one side is see-through. This is [the one we used](https://www.amazon.com/gp/product/B01CZ35XWY/ref=as_li_ss_tl?ie=UTF8&psc=1&linkCode=sl1&tag=gjhug1-20&linkId=5b62ea56680f9cf4a33e5db6234da0c4), it is 18" x 24" and 1mm thick, you want it to be pretty thin to make it easier for the light to shine through.
- Raspberry pi; we used a 3B, you will also need a micro SD card with a converter to go with it. You will need a micro-usb to usb and a usb power block for powering the pi. You will also need an HDMI to HDMI to connect the pi to the monitor.
    - You have the monitor but you will also need a usb mouse and keyboard to setup the pi, which you might have lying around anyway.
    - Optionally you can also get a case for the pi.

### Frame materials:
- Plywood 2x4s for the frame, we needed approximately 7ft with our plans which are later in this document
- Plywood sheets for the front part of the frame to make it look nice, and also for the back panel. You want to ask for the project board section in your local hardware store.
- Screws for putting the 2x4s together.
- Nails for nailing the plywood sheets to the front of the frame.
- Stain; the kind is up to you but we laser engraved part of our frame so to keep the engraving showing we used a lighter stain. You might want to just use a polyurethane coat to protect it.
    - You also need brushes to apply the stain/polyurethane.

### Sensor Related parts:
#### Gesture Parts
Our sensor work was based off of Thomas Bachmann's work and uses [his module](https://github.com/thobach/MMM-Gestures) for the Magic Mirror software. We also used the exact parts that [are listed in the hardware section of the readme](https://github.com/thobach/MMM-Gestures#hardware-setup) for the project. We have reproduced this list below.
- [Distance sensor:](https://www.amazon.com/GP2Y0A21YK0F-Sharp-Distance-10-80cm-Compatible/dp/B00IMOSEJA/ref=sr_1_sc_2?ie=UTF8&qid=1516763743&sr=8-2-spell&keywords=GP2Y0A21YK) GP2Y0A21YK, incl. connector cable
- [Gesture sensor:](https://www.amazon.com/Gowoops-APDS-9960-Recognition-Direction-Proximity/dp/B075651R2V/ref=sr_1_2?ie=UTF8&qid=1516763965&sr=8-2&keywords=APDS-9960
) APDS-9960 on breakout board with gesture sensor on one side, but no other electronic component on the same side for easier assembly (can be found on Aliexpress)
- [Micro-controller:](https://www.amazon.com/Elegoo-Board-ATmega328P-ATMEGA16U2-Arduino/dp/B01EWOE0UU/ref=sr_1_2_sspa?s=electronics&ie=UTF8&qid=1516765015&sr=1-2-spons&keywords=arduino+uno+with+usb&psc=1) Arduino (Uno), [incl. USB cable - male to male](https://www.amazon.com/UGREEN-Transfer-Enclosures-Printers-Cameras/dp/B00P0E394U/ref=sr_1_3?ie=UTF8&qid=1516765103&sr=8-3&keywords=usb%2Bto%2Busb&th=1)
- [Jumper cable](https://www.amazon.com/Haitronic-Multicolored-Breadboard-Arduino-raspberry/dp/B01LZF1ZSZ/ref=sr_1_1?ie=UTF8&qid=1516764623&sr=8-1&keywords=jumper+cable+arduino) to connect APDS-9960 with Arduino
- [Pin headers](https://www.amazon.com/OCR-Breakaway-Connector-Assortment-Arduino/dp/B01MQ48T2V/ref=sr_1_4?ie=UTF8&qid=1516764449&sr=8-4&keywords=pin+header) to solder to connector cable of GP2Y0A21YK

#### Audio Sensor Parts:
We are able to control the mirror using voice and get a response using audio so we needed a mic and speaker.
- [USB Microphone](https://www.amazon.com/eBerry-Adjustable-Microphone-Compatible-Recording/dp/B00UZY2YQE/ref=sr_1_6?ie=UTF8&qid=1516681229&sr=8-6&keywords=usb+microphone)
- [Bluetooth Speaker](https://www.amazon.com/NEWBEING-Wireless-Bluetooth-Handsfree-Slot%EF%BC%88Blue/dp/B0764CDY7Q/ref=sr_1_79?s=electronics&ie=UTF8&qid=1516682104&sr=1-79&keywords=speaker+bluetooth) NOTE: We used a Raspberry Pi 3B which has Bluetooth capability, if using an older version you will probably need a wired speaker.

# Software
We used a Raspberry Pi 3B, running raspbian. We used the open source Magic Mirror software and it's modules to drive our interface. 

## Setting up the Pi
First you need to get raspbian onto the SD card if it isn't already. Raspbian's site [has a great tutorial on how to do this](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) that we followed. Plug the SD card into the pi, also hook up the monitor, keyboard and mouse to the pi. Power the pi on and make sure that raspbian boots properly; then you can move on to installing the Magic Mirror software, [using their helplful docuementation](https://github.com/MichMich/MagicMirror#usage). Try to start up the Magic Mirror to make sure it works, de-bugging as necessary. Once you get that done you need to start to install the modules.

## Setting up Magic Mirror Modules
After setting up the Magic Mirror main software and getting the default setup to run, it's time to customize. We have the modules listed below, follow each link to the module's main page and follow their installation instructions. Any customizations to those modules will be listed below the list.

### List of Modules
- Default magic mirror - Mitch Mitch
- Add in ones for the sensors - link here
- thobach/MMM-Gestures
- Puns are in compliments.js
- clock - our timezone
- cal - to WiC calendar and multiple calendars bc they didn't have all of them
- weatherforcast - put in our location
- config - our modules and where they are on the screen

### Customizations/Settings for Modules
//TODO

# References
While researching this process we used many references including people who have done this kind of project before. We do this in the hopes that this may help future adventurers down this path.

- [Magic Mirror Central](https://www.magicmirrorcentral.com/making-a-magic-mirror/)
- [MagPi Magazine - Issue 54](https://www.raspberrypi.org/magpi/issues/54/)
- [Dylan Pierce blogpost Building MirrorMirror](http://blog.dylanjpierce.com/raspberrypi/magicmirror/tutorial/2015/12/27/build-a-magic-mirror.html)
- [Xonay Labs Michael Teeuw blog post](http://michaelteeuw.nl/post/80391333672/magic-mirror-part-i-the-idea-the-mirror)
