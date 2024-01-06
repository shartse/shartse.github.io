---
layout: page
title: "Building a Tide Clock"
permalink: /posts/tideclock
---
In the pre-Recurse, more free-form stage of my unemployment, I started going to the beach a lot more. I like looking for sea glass and sand dollars,
watching birds and poking around tide pools. This period included some "[Spring Tides](https://oceanservice.noaa.gov/facts/springtide.html)" or
 "King Tides" in San Francisco, where high tide was extra high and low tide extra low.
 Apparently, this happens when the Moon is directly between the Earth and the Sun (a new moon) and the gravitational pull of the Sun and the Moon are combined.
I saw some discussion of a whale skeleton that was buried a few years ago at Ocean Beach was now uncovered after historic amounts rains and visible (and very pungant) at low tide. Sadly, I did not find it before it was claimed by Cal Academy.
I read about and visited the "[Wave Organ](https://www.exploratorium.edu/visit/wave-organ)" which is apparently most audible at high tide.
One day, I'd like to hike the Lost Coast Trail, which involves a lot of tide awareness. Basically, I just started thinking about tides a lot more than normal.

# What determines tidal behavior?

Fundamentally, tides are caused the the gravitation forces exerted on water by the Moon and the Sun (apparently, these effects can also show up in the solid parts of Earth's surface a bit too, causing "terrestrial tides" - which makes exact global positioning extra hard). 

The Moon, being much close than the Sun, has a larger tidal impact. Throughout the day as the Earth rotates, the water that is closest to the Moon at
any given moment experiences the most pull and swells outward causing a high tide. The water on the exact other side of the Earth also bulges out.
This is confusing, but I think it's because it experiences the least pull and kind of drifts out a bit. This means that in ~24 hours, every place on Earth experiences two high tides.
The one close to the Moon is "high high tide" and the opposite is "low high tide". The Sun also exerts some gravitational pull on Earth's oceans, and when the Moon and Sun line up twice a month
(once on the same side of Earth, once on opposite sides) the tidal effects are amplified or dulled. This means the magnitude of a tide, known as the tidal range, changes throughout a month
and changes month to month depending on moon phases.

So far, all of this feel complicated but model-able with the right equations. However, tidal range (how high or low tides are) is also just really dependent on local conditions.
The shape of a coast line, the characteristics of the sea floor, the narrow-ness or wide-ness of an inlet all play into how high or low tides can get. This
is where NOAA's [Tide and Currents Predictions API](https://tidesandcurrents.noaa.gov/products.html) comes in. This API allows you to query tidal predictions for different
stations, in the past and the future.

# Project Idea
I wanted to make a simple display that shows daily tide information for my local beach. I started with no hardware or ebedded programming experience, so
I decided I wanted to try micro-controller programming and I wanted to learn more about ePaper (also known as eInk) technology, but I also wanted to minimize how much stuff I need to buy and new skills I needed.

# Materials 
This project makes use of a [Raspberry Pi Pico WH](https://www.raspberrypi.com/products/raspberry-pi-pico/) and a [Waveshare Pico ePaper](https://www.waveshare.com/wiki/Pico-ePaper-2.7) display.
Between the pre-soldered headers (the `H` of `Pico WH`) and the plug-in connection for the Pico headers on the ePaper Display (EPD), this project doesn't need any soldering.
The only other requirement is the micro USB cable, which should come with the Pico, to power and load code onto it.


# ePaper Background
ePaper was also a really interesting topic to learn about. I recommend perusing the [wikipedia article](https://en.wikipedia.org/wiki/E_Ink), but in
short, it's made of tiny, oil-filled cells with black and white oppositely charged particles. Applying a negative charge to a cell causes one color to rise
to the surface, a positive charge attracts the other color. Multi-color ePaper displays exist too - making using of different pigment particle sizes that
move at different rates. This physical system means ePaper has pretty different properties than other displays. For one thing, power is required to set
pixels, but once set, the screen can hold them without power. Another nice thing is that with pigment rather than light-based color, the display is really
easy on the eyes, matte and paper-like in a really satisfying way. Some downsides to this system is it's pretty susecptable to issues like ghosting - muddied
or residual colors from previous settings. This caused by a build up of charge on the display, so a full refresh is suggested pretty frequently and incremental
updates are harder.

