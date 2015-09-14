---
layout: default
title: First Prototype
category: builds
---

<h1>First prototype...</h1>

<p>For the first prototype I purchased a strip of APA102 "super LEDs".
In previous LED projects I'd been using the WS2812b (aka Neo-pixels) individually
controllable LEDs. I realised that these were probably not going to be fast
enough for fast moving effects so I invested in some APA102. I've not 
used these before but they're supported by the <a href="http://fastled.io/">FastLED library</a>
I was using before, so getting up and running with them was really easy. 
</p>

<p>Here's what my first version look like:</p>

<figure>
  <img src="{{site.baseurl}}/img/poi-3.jpg" alt="Prototype 1">
</figure>

<p>As you can see, a very rough prototype. I used PVC waste pipe and cut a 180mm length. drilled a couple of 
holes to tie the cord on with. I used double sided tape to attach the LED strip. I had to adjust the LED positioning
a couple of times to get it right, so the tape lost it's stickiness a bit. That's why you can see a couple of cable
ties securing down the ends of the LED strip. I adjusted the strip a few times because I was trying to evenly 
spread the LEDs by coiling it around the pipe in such a way that the LEDs lined up. The best I could get on this
version was to have them interleave on each turn around the pipe. I'll improve this on the next version.</p>

<p>You can also see I'm using gaffa tape to secure the end to stop the insides flying out as you 
spin them. I've got plans to improve this for the next version. </p>

<p>In this photo you can see what's inside the first version.
</p>

<figure>
  <img src="{{site.baseurl}}/img/poi-4.jpg" alt="Prototype 1 - insides">
</figure>

<p>Power comes from a pair of AAA batteries, boosted to 5v using a Powerboost 500.
The Powerboost has a handy USB socket, into which I plugged the Digispark controller 
to power it. It's easily removed to plug into the computer for programming. 
</p>

<p>The APA102 strip is connected to the Digispark 5V power and GND. The DATA line
is soldered to P0, and the CLOCK soldered to P2.</p>

<p>This is a simple but effect construction to get up and running.</p>

<p>Here's a photo of the first prototype after tidying it up a bit, removing the 
cable ties and redoing the double sided tape:</p>

<figure>
  <img src="{{site.baseurl}}/img/poi-5.jpg" alt="Open source LED Poi - Prototype 1">
</figure>

<p>Each poi has 36 LEDs and weighs 88g (inc 2x AAA batteries).
They're pretty robust. The batteries came out of the holder after I hit myself on the back of the head with them
(yes - I'm still learning!) but the batteries can easily be made more secure.</p>

<p>It works! but need better photos. The camera on my phone doesn't do it justice...</p>

<figure>
  <img src="{{site.baseurl}}/img/poi-6.jpg" alt="DIY LED Poi">
</figure>

<h1>Software</h1>

<p>The Digispark is compatible with the Arduino IDE so programming simple sketches 
is easy. </p>

<p>I uploaded a few example patterns to GitHub in this 
<a href="https://github.com/PoiOS/simple-poi">simple-poi</a> repository.</p>

<p>Eventually, I want to make the device programmable without coding so that users
without technical ability will be able to programme their own patterns. This will be acheived by
writing a simple OS software that runs a special byte sequence. This sequence 
is a simple programme that can be compiled and uploaded from simple scripts, 
or via a GUI interface.</p>

<p>The byte sequence needs to be able to store patterns, timings, and effects.
A simplified instruction set should allow some complex patterns and effects to 
be encoded.</p>