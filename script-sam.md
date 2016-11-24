**UPDATE LIVEJS WEBSITE WITH PROJECTS AND GITHUB LINKS**

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

...modV!

modV stands for Modular Visualisation. It is an Open Source audio visualisation environment written in JavaScript and runs in Google Chrome.

## modV: Canvas

CanvasRenderingContext2D, or Canvas 2D for short, is used for drawing simple shapes and copying image data onto ```<canvas>```.

Incredibly, ```<canvas>``` counts as image data too, so we can draw Canvas back onto itself.  
If we stretch the image as well we can create the the age old effect of infinite video loops: the tunnel effect.

Usually in modV, I use Canvas2D to create source blocks of colour and lines that can be manipulated by the other modV Module types.

## modV: WebGL

modV uses WebGL in two different ways.  
Again, standing on the shoulders of giants, I've used THREE.js as modV's 3D engine.

Any 3D models seen within modV will use THREE.js.

*Added from the slide*: modV uses THREE.js for 3D models and complex 3D scenes.

## modV: GLSL

*Added from the slide*: OpenGL Shader Language, GLSL for short, can process pixel data on the GPU extremely fast.

However, modV can also process anything drawn onto the screen as a WebGL texture and modify that using GLSL (OpenGL Shader Language) using the client's graphics processor.  
This allows for incredible effects that would otherwise not be possible using Canvas2D.

(*EXAMPLES OF SHADERS*)

**MOVE TO LIVEJS DOTJS GITHUB**

A great resource for learning GLSL is the Book of Shaders by by Patricio Gonzalez Vivo and Jen Lowe.  
Check it out at: http://thebookofshaders.com/

**END MOVE TO LIVEJS DOTJS GITHUB**

## modV: Modules

So, we've covered the visualisation technologies - but how can we put all of this together in an ***EASY TO USE*** API?

That's where the modular part of modV comes in.  
modV has a collection of four different types of Modules at the moment:

* Module2D - Canvas2D
* Module3D - THREE.js (WebGL)
* ModuleShader - GLSL (WebGL)
* ModuleScript - Canvas2D + GLSL (WebGL)

## modV: Putting all of this together

When combined, these Modules can create some stunning visuals.

(**Show off Module Types in Demo 5 - 10 seconds 🎉**)

(**DEMO TIME**)

# TIM SPEAKS

## Combination Pizza Hut and Taco Bell

**SAM:** Tim and I met through Live:JS, a collective of audio and visual artists who *build live experiences, shows and installations*, a couple of months ago.  

**TIM:** Sam travelled to Germany to meet me in person, and we combined our projects in a hack weekend. (*PICTURE*)

**SAM:** We added MIDI controller assignments in modV and grabbed the Canvas data to send it over WebSockets to nerdV, controlling the LEDs and DMX!

**???:** And tonight, in this sweet venue, in Paris, we're going to rock this conference.

(*LOGOS COME TOGETHER -> EXPLOSION -> FADE TO BLACK -> SWITCH TO MODV BLACK SCREEN*)  
(*SAM TO FIGURE OUT SWITCHING BETWEEN SLIDES AND MODV*)
