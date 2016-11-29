# LiveJS : dotJS

* Hi, my name is Sam
* and my name is Tim

our story is split into 3 chapters and by the end you will know how to use the web to do an audio / visual live performance. 


---

# Part 1: Sam



---

# Part 2: Tim

## NERDDISCO

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

(Create a MIDI device demo)
(Add pics of the devices I'm using)
(calculate the avg value from the LED array)






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





# Snippets


* Since then I'm gave talks about NERD DISCO around the world to inspire everyone to be creative with the web
* In the last couple of months I started to collaborate with other web artists, like Sam, to get even 

* Since then I talked about NERD DISCO around the world
* My passion is music too. But instead of using Game Boys, I use the browser. 

* When I was 10 my parents gave me a drum set for my birthday and I loved to play it every day. (pic of me playing drums)
* 10 years later I had to sell it to finance my information science studies and that made me very sad
* After leaving the university, I was still sad, so I got a cat and named him Kazzo. He loves to talk with me at night and at some point he told me:

**Kazzo** You love music and you are a dev, why don't you create something based on that?
**Tim** That is a really good idea.

* That conversation happened more than two years ago and shortly after I started NERD DISCO.
* It's using **Web Audio** to analyse music and **Canvas** to generate visualisations, but as Sam already talked about that in his software **modV** in depth, I want to focus on the hardware side of NERD DISCO.




* More than two years ago I started NERD DISCO: A project to generate visualize audio by using web technologies.
* These visualiaztions are generated on canvas  And because Sam already talked about how modV generated visualizations, I will focus on the hardware side of NERD DISCO:

* A project to visualize audio in the browser using canvas and on LEDs
* In the beginning it was just audio analysing combinded with simple visuals on LEDs

Over the time the project evolved:

* canvas to create more complex visuals (add pic)
* I build different LED prototypes (add pic)
* Improved the web UI
* Added MIDI devices to control the visualizations


# MIDI

Instead of using an advanced browser UI, I wanted to use real hardware like this KORG padKONTROL:

* And thanks to the **Web MIDI API** I can use that
In JavaScript we can control any MIDI device with the help of the **Web MIDI API**.

* Request access by using `navigator.requestMIDIAccess`
* And handle the `MIDIMessageEvent`


# LED curtain

* My Node.js-app called [nerdV](https://github.com/NERDDISCO/nerdV) is running on the Raspberry PI and it's purpose is to
	* Creates a WebSocket-server
	* Send the RGB colors that it gets over WebSocket-Connection over USB to the FadeCandy


# DMX

---
REMOVE

* Each DMX network (called universe) is managed by a single DMX controller and can have one ore more slave devices
* The slaves are chained together and the signal is transfered from device to device

![https://commons.wikimedia.org/wiki/File:SimpleDmxUniverse.gif](https://upload.wikimedia.org/wikipedia/commons/6/62/SimpleDmxUniverse.gif)

REMOVE
---
