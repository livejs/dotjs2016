# LiveJS : dotJS

* Hi, my name is Sam
* and my name is Tim

our story is split into 3 chapters and by the end you will know how to use the web to do an audio / visual live performance. 




---

# Part 1: Sam


## Game Boy music

So right off the bat, we're not going to talk about JavaScript.  
Instead, let's talk about a passion of mine.

![nanoloop 2](https://scontent-frt3-1.cdninstagram.com/t51.2885-15/s640x640/e15/14063636_1205327192868611_650892397_n.jpg?ig_cache_key=MTMyODI5NTMzMTU3ODcyODc5OQ%3D%3D.2)

I use the Nintendo Game Boy to create music, which is commonly referred to as Chiptune.  
I've played shows with my music all over Europe and it sounds a little like this:

(*PLAY MUSIC*)

I've been doing this for about 8 years now, and just a couple of years ago I wanted to create visuals to go with my music and shows.

As there is no direct MIDI output from the software I use on Game Boy, I researched how to analyse audio using JavaScript in the browser.


## WebAudio analysing

The WebAudio API is an adaptable system for controlling, analysing and processing audio on the web.  
It is a node-based system (*SHOW DIAGRAM*), allowing the audio to "flow" through different connections. If you've ever used PureData, Max MSP or Blender you should be familiar with this.

We start off with an **audio context**, and add from there.  
For basic usage, a source is needed and a destination.

Sources can be either ```<audio>```, an oscillator or a stream.  
The destination is usually your speakers, but can be any audio output your system supports.

In between the input and output we can add other nodes such as effects (reverb, biquad filter, panner, compressor), gain nodes and, what I needed for visualisation, analyser nodes.

(*ANALYSER NODE INFORMATION*)

You can do a lot with the Analyser node on its own but there comes a point where I needed a more refined value to work with.  
I use Meyda, the audio processing library by Hugh Rawlinson, Nevo Segal and Jakub Fiala.  
Meyda can return far more advanced audio analysis (*LIST OF MEYDA'S FEATURES*) and the two which are most useful to me are ZCR, the Zero Cross Rate and RMS, Root Mean Squared.

ZCR is great for detecting high frequency percussive elements such as high hats and RMS is very good at detecting the kick drum in a song.


## modV

modV stands for Modular Visualisation. It is an Open Source audio visualisation environment written in JavaScript and runs in Google Chrome.

The program is the result of my 2 year adventure into audio visualisation using JavaScript.

### Canvas

CanvasRenderingContext2D, or Canvas 2D for short, is used for drawing simple shapes and copying image data onto ```<canvas>```.

Incredibly, ```<canvas>``` counts as image data too, so we can draw Canvas back onto itself.  
If we stretch the image as well we can create the the age old effect of infinite video loops: the tunnel effect.

Usually in modV, I use Canvas2D to create source blocks of colour and lines that can be manipulated by the other modV Module types.


### WebGL

modV uses WebGL in two different ways.  
Again, standing on the shoulders of giants, I've used THREE.js as modV's 3D engine.

Any 3D models seen within modV will use THREE.js.

*Added from the slide*: modV uses THREE.js for 3D models and complex 3D scenes.


### GLSL

modV can also process anything drawn onto the screen as a WebGL texture and modify that using OpenGL Shader Language, GLSL for short. GLSL code runs on client's graphics processor.
This allows for incredible effects that would otherwise not be possible using Canvas2D.


## Modules: Putting all of this together

So, we've covered the visualisation technologies - but how can we put all of this together in an ***EASY TO USE*** API?

That's where the modular part of modV comes in.  
modV has a collection of four different types of Modules at the moment:

* Module2D - Canvas2D
* Module3D - THREE.js (WebGL)
* ModuleShader - GLSL (WebGL)
* ModuleScript - Canvas2D + GLSL (WebGL)

(**Show off Module Types in Demo 5 - 10 seconds 🎉**)

When combined, these Modules can create some stunning visuals.

(**DEMO TIME**)
---

# Part 2: Tim

## NERDDISCO


* Experiment with ND and collaborate with other people
* 

* My passion is music too. But instead of using Game Boys, I use the browser. 

* When I was 10 my parents gave me a drum set for my birthday and I loved to play it every day. (pic of me playing drums)
* 10 years later I had to sell it to finance my information science studies and that made me very sad
* After leaving the university, I was still sad, so I got a cat and named him Kazzo. He loves to talk with me at night and at some point he told me:

**Kazzo** You love music and you are a dev, why don't you create something based on that?
**Tim** That is a really good idea.

* That conversation happened more than two years ago and shortly after I started NERD DISCO.
* It's using **Web Audio** to analyse music and **Canvas** to generate visualisations, but as Sam already talked about that in his software **modV** in depth, I want to focus on the hardware side of NERD DISCO.


## 1. Web MIDI

* MIDI stands for **Musical Instrument Digital Interface** and is a standard that defines protocols and connectors
* It's main purpose is to connect electronic instruments, computers and other MIDI devices with each other
* Like this **KORG nanoPAD2**

![](http://cdn.korg.com/us/products/upload/cc214ae500c828839b5dd93d23786f39_pc.jpg?Expires=1482182996&Signature=QqVmvFaF4Lei5JIawEeJyeXr2Tm58YSO4r42CHMv0AHQLOfejB7nQCaAOKpQX6dHTMDlzItFBwLEpHHplgk2hIY75F1dhL-d0zlWmy~HNbH-il8Wjx6O3sA4i87OrxN93qbe8toj3AGZe~qqNadDRcJVhF~M55XcxRGCPH50pLAQzOV56vnwFq1fGdyeqXxGaAGyJB020qVjmQfEhFznjG7ylLm9J5n2fGMDx3aYltLCYTN~0C~kS2dhiKtgZc~a0GVmTUZLkUG9DkWs42JpP3iQCKacgfqYGBUC9R0t4oK~vrOX-9P32c~28eO0rm1TRwwADr2hCV6Jywfrb4oyRw__&Key-Pair-Id=APKAIQGL3XAA7HGZGU6Q)

* It is small, can be connected over USB to the computer and it can be used in the browser by using the **Web MIDI API**

### Demo: MIDI

(open *MIDI Console*)

* To play around with the **Web MIDI API** I created the **MIDI Console**
* When you connect a MIDI device you can see it's manufacuter and it's name
* In this case it's the **nanoPAD2** from **KORG**
* And if I push one of the buttons, you can see the prettyfied data from the **MIDIMessageEvent**
* When I release the button, another **MIDIMessageEvent** is fired
* When the button is pushed, the command name is noteOn
* When the button is release, the command name is noteOff
* Every button has a unique note, so I can identify which button was triggered
* That means we can use MIDI devices to control software in the browser


(add transition to LED)

## 2. LED Curtain

One way to get the visualizations from the screen into the real world is to use LEDs. And because I love to create prototypes, I build this LED curtain:

![](https://s3.amazonaws.com/media-p.slid.es/uploads/11681/images/2981468/led_curtain_1920.JPG)

It consists of

* 8 strips with 30 LED per strip (Adafruit NeoPixel)
* 1 FadeCandy to control the LEDs
* 1 Raspberry PI to control the FadeCandy over USB
* Raspberry PI is running a Node.js-app called [nerdV](https://github.com/NERDDISCO/nerdV), which creates a WebSocket-Server and provides an API to send RGB colors to it
* 1 WIFI router to control the Raspberry PI remotely from my computer


### Demo: MIDI + Canvas + LED

* This is NerdDrum
* The black square is an **canvas** element
* The 8 white rectangles are a visual represenation of the 8 **LED strips**
* This means that each strip on the screen is mapped to one **LED strip**
* If I push a button on the **KORG nanoPAD2**, a rectangle is drawn onto the **canvas** and moves from the top to the bottom
* When I activate the WebSocket-Connection to the Raspberry PI, you can see that the colors from the canvas are send to the corresponding **LED strip**



## 3. DMX512

If you want to control lights, but don't want to build everything yourself, you can use DMX512

* DMX stands for **Digitial Multiplex**
* It's a standard for digital communication networks and it's commonly used to control stage lightning like in this theatre:

![Fir0002/Flagstaffotos](https://upload.wikimedia.org/wikipedia/commons/c/cb/Classical_spectacular10.jpg)

All the lights and lasers are controlled using DMX512

* Unfortunately there is no JavaScript-API yet to control DMX in the browser, but we can use **Node.js** in combination with a USB DMX controller to manage DMX devices

![Enttec USB DMX controller](https://www.thomann.de/pics/bdb/345648/11007641_800.jpg)


### Demo

* My Node.js-App [nerdV](https://github.com/NERDDISCO/nerdV) can also be used to control DMX512
* Send RGB colors over WebSocket to change the color of the Stage Lights
* Turn on / off fog machine
* Maybe use a MIDI device





---

# Part 3: Sam + Tim

**SAM:** A couple of months ago, Tim and I met through Live:JS: A collective of audio and visual artists. And then I asked Tim: Oh, wouldn't it be nice to combine our projects? 

**TIM:** YES, that is a good idea. Let's have a Hack Weekend. 

**SAM:** We added MIDI controller assignments in modV and grabbed the Canvas data to send it over WebSockets to nerdV, controlling the LEDs and DMX! 

**TIM:** But tonight, in this sweet venue, in Paris, we're going to rock this conference. 



##  Show





---

# The End

**TIM:** You can find us online whatever

**SAM:** If have any question just tweet @rumyra

**TIM:** Thank you very much. This is the End. 

**SAM:** GOOOOOOOOOD BYE!

**TIM:** BOOOM HEADSHOT!!!

✨
