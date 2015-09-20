---
layout: default
title: Second Prototype Parts and Specs - more details
category: builds
og_image: http://poios.org/img/2nd/05.jpg
---

# Second Prototype Specs

Here's some specs of the basic pixel poi 
(second prototype) as detailed [here](/builds/2015/09/18/second-prototype.html)... 

 * Resolution: 8 pixels (16 LEDs in total on each poi)
 * Weight: 115g each (inc batteries)
 * Length: 240mm

Cost of parts required for each poi...

 * Powerboost 500B = £11 each
 * Arduino Nano = &pound;2.95 (cheap Chinese clone)
 * Foam board = &pound;0.00 (cut from scrap)
 * Silicone Hose End Blanking Caps = &pound;11.34 (pack of 10)
 * 32mm diameter black Polypropylene waste pipe = &pound;3.99 (25cm length)
 * APA102 Addressable RGB LED strip = &pound;19.98 for 1m (72 LEDs per metre)
 * SPDT ON-Off Miniature Slide Switch = £1.99 (for 20)
 * AAA battery holder = £4.89 for 5
 * 28mm Clear Acrylic tube = £5.99 for 250mm


## Compatibility

The cheap Chinese version of the Arduino Nano wasn't reconised by my Mac.
After a bit of research I found out that the USB driver chip used is
different to the standard Arduino (to get around licensing issues) and
requires a special driver. 

Even after installing the driver I was unable to programme the Nano,
but after a bit more googling I found [this post](http://0xcf.com/2015/03/13/chinese-arduinos-with-ch340-ch341-serial-usb-chip-on-os-x-yosemite/) that pointed out the 
issue with the space character in the serial port name. 
