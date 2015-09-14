---
layout: default
title: First attempt at Poi operating system code
category: code
---

<h1>Poi OS - First attempt at Poi OS code</h1>

<p>Here's a first experiment with creating a general purpose 
OS code for the LED Poi that will allow customised programmes to
be uploaded and run on the Poi.</p>

<h1>Design ideas</h1>

<ul>
  <li>A "programme" is a list of commands and parameters</li>
  <li>Commands will allow setting LED colours, manipulating colour palettes, delay, fades, strobes, etc</li>
  <li>A default programme is provided, in future will allow programmes to be uploaded to the device from a separate app on computer.</li>
</ul>

<h1>First attempt at code</h1>

<p>Here's an idea as to how this might work. The main loop reads the programme counter (```pc```) variable to work out the current instruction to execute. It calls the appropriate command function (passing in any provided parameters), then increases the programmme counter to the next instruction.</p>

{% highlight c++ %}
#include "FastLED.h"

#define NUM_LEDS 36
#define DATA_PIN 0
#define CLOCK_PIN 2
#define PROG_SIZE 128

// Instruction set command numbers
#define CMD_SET 0 // requires 3 parameters: colorIndex, start, end
#define CMD_WAIT 1 // requires 1 parameter: delay (in ms)
#define CMD_CLEAR 2 // requires 0 parameters
#define CMD_SHOW 3 // requires 0 parameters
#define CMD_END 4 // requires 0 parameters

CRGB leds[NUM_LEDS];

// A programme is a list of instructions.
// Each instruction is a command byte followed by a 
// list of parameters. The number of parameters varies
// depending on the command.
const PROGMEM  uint8_t defaultProg[] = { 
  19, // First number is length of programme
  CMD_SET, 0, 0, 36,
  CMD_SHOW,
  CMD_WAIT, 1000,
  CMD_CLEAR,
  CMD_SET, 128, 18, 36,
  CMD_SHOW,
  CMD_WAIT, 1000,
  CMD_CLEAR,
  CMD_SHOW,
  CMD_WAIT, 1000
};

CRGBPalette16 currentPalette;
TBlendType currentBlending;
uint8_t currentProg[PROG_SIZE];
uint8_t pc; // programme counter

void setup() {
  FastLED.addLeds<APA102, DATA_PIN, CLOCK_PIN>(leds, NUM_LEDS);
  FastLED.clear();

  // If programe has been uploaded to EEPROM use that, here we use default
  // programme stored in PROGMEM and copy to currentProg
  uint8_t iMax = pgm_read_byte_near(defaultProg) + 1;
  for (uint8_t i = 1; i < iMax; ++i) {
    currentProg[i - 1] = pgm_read_byte_near(defaultProg + i);
  }
  // Terminate programme with END command (loop back to beginning)
  currentProg[iMax] = CMD_END;
  currentPalette = PartyColors_p;
  currentBlending = BLEND;
  pc = 0;
}

void setLEDs(uint8_t colorIndex, uint8_t startLED, uint8_t endLED) {
  CRGB col = ColorFromPalette(currentPalette, colorIndex, 255, currentBlending);
  for (uint8_t i = startLED; i < endLED; ++i) {
    leds[i] = col;
  }
}

void loop() {
  switch(currentProg[pc]) {
    case CMD_SET: 
      setLEDs(currentProg[pc + 1], currentProg[pc + 2], currentProg[pc + 3]);
      pc += 4; // jump to next instruction in programme
      break;
    case CMD_WAIT:
      FastLED.delay(currentProg[pc + 1]);
      pc += 2;
      break;
    case CMD_CLEAR:
      FastLED.clear();
      pc++;
      break;
    case CMD_SHOW:
      FastLED.show();
      pc++; 
      break;
    case CMD_END:
      pc = 0;
      break;
  }
  if (pc >= PROG_SIZE) pc = 0;
}
{% endhighlight %}

