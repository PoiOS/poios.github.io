---
layout: default
title: LED Pixel Poi POV demo
category: code
og_image: http://poios.org/img/2nd/05.jpg
---

# LED Pixel Poi - First POV experiments

Now I've got a basic version of the pixel poi working I can 
start experimenting with POV (persistence of vision) effects.
The second prototype poi have an 8 bit resolution, but that's
enough to start creating some simple effects.

<figure>
  <img src="{{site.baseurl}}/img/2nd/demo5.jpg" alt="LED Pixel Poi POV demo 5">
</figure>

<figure>
  <img src="{{site.baseurl}}/img/2nd/demo1.jpg" alt="LED Pixel Poi POV demo 1">
</figure>

Here's some code that displays a simple hard-coded pattern. 
It uses the FastLED libraries colour palette functionality, and has the 
pattern as a simple array of palette indexes. 

The palette has 16 colours, and index 99 is used to turn off an LED. 

{% highlight c++ %}
#include "FastLED.h"

#define NUM_LEDS 16
#define DATA_PIN 4
#define CLOCK_PIN 5
#define BRIGHTNESS 255
CRGB leds[NUM_LEDS];

CRGBPalette16 currentPalette;
TBlendType currentBlending;

#define PROG_SIZE 48
uint8_t pattern[] = {
  99, 99, 99,  1,  1, 99, 99, 99,
  99, 99,  1,  2,  2,  1, 99, 99,
  99,  1,  2,  3,  3,  2,  1, 99,
   1,  2,  3,  4,  4,  3,  2,  1,
  99,  1,  2,  3,  3,  2,  1, 99,
  99, 99,  1,  2,  2,  1, 99, 99,
  99, 99, 99,  1,  1, 99, 99, 99,
  99, 99,  1, 99, 99,  1, 99, 99,
  99,  1, 99,  5,  5, 99,  1, 99,
   1, 99,  5, 99, 99,  5, 99,  1,
  99,  1, 99,  5,  5, 99,  1, 99,
  99, 99,  1, 99, 99,  1, 99, 99,
};


void setup() {
  FastLED.addLeds<APA102, DATA_PIN, CLOCK_PIN>(leds, NUM_LEDS);
  FastLED.clear();
  currentPalette = PartyColors_p;
  currentBlending = BLEND;
}

void loop() {
  static uint8_t startIndex = 0;
  for (uint8_t i = 0; i < 8; ++i) {
    CRGB c;
    if (pattern[startIndex] == 99) {
      c = CRGB::Black;   
    }
    else {
      c = ColorFromPalette(currentPalette, pattern[startIndex] * 32, BRIGHTNESS, currentBlending);
    }
    leds[i] = c;  
    leds[15 - i] = c;
    startIndex += 1;
    if (startIndex == PROG_SIZE) startIndex = 0;
  }
  FastLED.show();
  FastLED.delay(5);
}
{% endhighlight %}
