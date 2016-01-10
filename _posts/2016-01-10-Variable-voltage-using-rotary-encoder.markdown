---
layout: post
title: 'Variable Voltage Reference'
categories: electronics embedded
tags: pic12f683 variable voltage rotary encoder
published: true
---

There are times when you need to generate a variable voltage reference in order
to test something in an electronic circuit. For example, you might have an
op-amp based current sink for which you should be able to modify the value
of the current by varying the voltage at its non-inverting input. Sure, you can
use a *bench-top power supply* but what if you don't have one? Or what if you
want to have a more precise control of the variable voltage, down to a few millivolts?  

### __Requirments__

This little circuit uses:

- 1 x microcontroller (I chose the PIC12f683)
- 1 x 24-step
rotary encoder (any number of steps will do)
- 2 x 10k resistor
- 1 x 100k resistor
- 1 x 68nF capacitor

in order to make a simple PWM-based voltage reference with about 20mV resolution at 5V input voltage.

### __Principle of operation__
#### _**Filter**_

![Block scheme](/static/posts-images/var-voltage-block.png)

For the filter I'll implement an RC low-pass filter such that the frequency of my PWM (15.625kHz) will be attenuated by at least -48dB. Why -48dB? Because that would mean an attenuation of around 250, which would mean that a 5V peak-to-peak square wave will generate less than 20mV of ripple at my filter output. This means the cutoff frequency for my filter would need to be around 62.5Hz. I choose `R = 100k` and `C = 68nF` leading to a cutoff frequency of `fc = 23.4 Hz`.  This leads to an attenuation of around -56dB meaning a ripple of about 8mV peak-to-peak at the output.

#### _**Rotary encoder**_

My rotary encoder has three pins (A, B and COM) and is connected like this:
![Schematic of the encoder](/static/posts-images/encoder-schem.png)
A and B are connected to digital inputs on my microcontroller.

This is how a rotary encoder works:
![Courtesy of electro-labs.com](/static/posts-images/rot-encoder.png)

Let's assume you view A and B through an oscilloscope. COM is connected to GND. A and B are connected to VCC through a pull-up resistor. __When you rotate the encoder you'll see square waves both on A and B__. The direction of rotation, however, is encoded in the phaseshift of those two waveforms.
When the encoder is rotated clockwise, A will be shifted ahead of B. When rotated counter-clockwise, the opposite is true. So in order to determine the direction of rotation we must choose an edge, for example the falling edge of A, and see the value of B on that edge.  
When we are at the __falling edge of A and B is 1__, that means we're rotating __clockwise__. When, however, we're at the __falling edge of A and B is 0__, that means we're rotating __counter-clockwise__.

### __The circuit & software__
![](/static/posts-images/circuit.png)
The microcontroller reads if the encoder was rotated clockwise or counter-clockwise,
increments or decrements an internal variable which sets the PWM value on Pin 5 of
the PIC. The __PWM__ resolution is __8 bits__ and the frequency __15.625kHz__.  
Connected to Pin 5 is the low pass filter and the DC output is taken directly
from the capacitor, therefor this circuit cannot drive any load. It can only
be used as a voltage reference.

__[Here](https://github.com/Ardelean-Calin/Rotary-Encoder)__ is the code for the
PIC12f683.

I have soldered the circuit on a small perfboard.
![](/static/posts-images/soldered.jpg)

### __Conclusion__
Well, this is it. The circuit works well and satisfies my needs. I used it in order to make a variable current sink. I would measure and post the performances here, however I do not have an oscilloscope and showing a bunch of multimeter screens
wouldn't really bring any more useful information to this post.  
__Hopefully you enjoyed/learned something from this project! Stay tuned for more!__

___Note:__ This was my first post on this site. I wanted to
test Jekyll and GitHub Pages and have the site up and running so that I can more easily publish more posts in the future. I also wanted to get a grip on how to format my blog posts.  
I will try to make the next ones much better! Thank you for reading! :)_
