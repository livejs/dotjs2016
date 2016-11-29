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

* My two biggest passions are music visualizations and experimenting with web technologies
* To combine both these passions into one project I started NERD DISCO more than two years ago
* Since then I gave talks around the world to inspire everyone to be creative with the web
* Recently I also started to collaborate with other web artists to reach new creative horizons. 
* One of them is Sam and because he already explained how to create visualisations, I will focus on the hardware side of NERD DISCO. 



## 1. MIDI

* Let's start with MIDI, which stands for **Musical Instrument Digital Interface**
* It's a standard that defines a data protocol and adapters
* And it's main purpose is to connect electronic instruments, computers and other MIDI devices with each other
* In the browser we have the **Web MIDI API**, which makes it possible to use any MIDI device over USB, like this **KORG nanoPAD2**
* We only need to **requestMIDIAccess**
* And listen to **MIDIMessageEvent**'s
* Which are fired every time we use a button or an other input on the MIDI device
* That makes it super easy to control any software 



## 2. LED Curtain

Another main part of NERD DISCO are LEDs and because I love to create prototypes, I build this LED curtain:

![](https://s3.amazonaws.com/media-p.slid.es/uploads/11681/images/2981468/led_curtain_1920.JPG)

It consists of

* 8 strips with 30 LED per strip, the LEDs I'm using are called NeoPixel. The cool thing about them is that they can display any RGB color we want
* To manage the LED strips I'm using a microcontroller called FadeCandy and it was only build to control NeoPixels 
* The FadeCandy is connected over USB to a Raspberry PI and the Raspberry PI is running a Node.js-app, which can send data to the FadeCandy over USB and creates a WebSocket-Server, so I can control the Raspberry PI over WIFI from my computer

* The FadeCandy expects an array of 3-byte triples for each LED 
* For example to light up the first LED with red and the second LED to green, we have to send this array

array(
  /* 1 LED */ 255, 0, 0, 
  /* 2 LED */ 0, 255, 0
)



## 3. DMX512

* If you don't want to build your own lights, you can use DMX512
* DMX stands for **Digitial Multiplex** 
* It's a standard for digital networks and it's commonly used for professional lightning, like you can see in this theatre: all the lights and lasers are controlled using DMX
* 
* The 512 stands for 512 channels, so each DMX512 universe  can have 512 seperate channels
* Every channel has 1 byte
* My DMX512 universe consists of a USB DMX Interface, 2 PAR lights and a fog machine
* I have a Node.js-app running on my computer, which can talk over USB to the DMX interface
* The DMX interface expects an array of 512 bytes
* Each DMX device can have multiple channels and a configured address
* The devices are connected in series
* The PAR lights have 3 channels each, which means the first one is at address 1, the second one at address 4, the fog machine at 7. 
* If I want to turn the first PAR light to red, I send the following array

array(/* PAR light A */ 255, 0, 0,
      /* PAR light B */ 0, 0, 0,
      /* fog machine */ 0)
      
* To change also change the color of the second PAR light to green and turn on the fog machine, I send the following array:

array(/* PAR light A */ 255, 0, 0,
      /* PAR light B */ 0, 255, 0,
      /* fog machine */ 255)





---

# Part 3: Sam + Tim

**SAM:** A couple of months ago, Tim and I met through Live:JS: A collective of audio and visual artists. And then I asked Tim: Oh, wouldn't it be nice to combine our projects? 

**TIM:** YES, that is a good idea. Let's have a Hack Weekend. 

**SAM:** We added MIDI controller assignments in modV and grabbed the Canvas data to send it over WebSockets to nerdV, controlling the LEDs and DMX! 

**TIM:** But tonight, in this sweet venue, in Paris, we're going to rock this conference. 



##  Show





---

# The End

**TIM:** You can find us online on livejs.network

**SAM:** If have any question just tweet @livejs_network

**TIM:** Thank you very much. This is the End. 

**SAM:** GOOOOOOOOOD BYE!

**TIM:** BOOOM HEADSHOT!!!

✨
