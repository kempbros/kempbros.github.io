---
layout: post
author: benjamin
title: IKEA/Teenage Engineering FREKVENS 6x10 Teardown
description:
modified: 2020-01-25
tags: [ikea te teenage engineering teardown bluetooth tiny things]
categories: [Bluetooth Audio]
image:
    feature: 00_6x10_title.jpg
excerpt: IKEA FREKVENS 6x10 teardown
---

## Unboxing & Teardown:
Curious about the innards of the Teenage Engineering designed IKEA FREKVENS 6x10?  I was and thought I'd share.  It's a little bluetooth speaker box running on a ATS2815 "single chip bluetooth solution". 

<figure class="half center">
	<a href="/images/FREKVENS/01_6x10_box.jpg"><img src="/images/FREKVENS/01_6x10_box.jpg" alt=""></a>
	<figcaption>The lovely IKEA packaging.</figcaption>
</figure>
	
Now, I'm not really in the mood to elucidate, so here's a bunch of pix.  My main goal for this excursion was to see if there is room to fit a Teensy 3.2 inside of the enclosure.  I think the answer is basically, no, but there is a bit of room for a small package.  You'd have access to power and a speaker, so I'm tempted to cram something in there...

<figure class="half center">
	<a href="/images/FREKVENS/02_6x10_box.jpg"><img src="/images/FREKVENS/02_6x10_box.jpg" alt=""></a>
	<figcaption>The lovely IKEA packaging.</figcaption>
</figure>

<figure class="half center">
	<a href="/images/FREKVENS/03_6x10_opened.jpg"><img src="/images/FREKVENS/03_6x10_opened.jpg" alt=""></a>
	<figcaption>Watcha get inside the box.</figcaption>
</figure>

<figure class="half center">
	<a href="/images/FREKVENS/04_6x10_top.jpg"><img src="/images/FREKVENS/04_6x10_top.jpg" alt=""></a>
	<figcaption>The top.</figcaption>
</figure>

<figure class="half center">
	<a href="/images/FREKVENS/05_6x10_side.jpg"><img src="/images/FREKVENS/05_6x10_side.jpg" alt=""></a>
	<figcaption>The side.</figcaption>
</figure>

<figure class="half center">
	<a href="/images/FREKVENS/06_6x10_back.jpg"><img src="/images/FREKVENS/06_6x10_back.jpg" alt=""></a>
	<figcaption>The back.</figcaption>
</figure>

<figure class="half center">
	<a href="/images/FREKVENS/07_6x10_stuff.jpg"><img src="/images/FREKVENS/07_6x10_stuff.jpg" alt=""></a>
	<figcaption>The stuff.</figcaption>
</figure>

<figure class="half center">
	<a href="/images/FREKVENS/08_6x10_opening.jpg"><img src="/images/FREKVENS/08_6x10_opening.jpg" alt=""></a>
	<figcaption>This thing was a pain to open.  It has two clips on the front and two on the back.  I had success using a guitar pick as a prybar and didn't end up breaking anything.</figcaption>
</figure>

<figure class="half center">
	<a href="/images/FREKVENS/09_6x10_opening_front.jpg"><img src="/images/FREKVENS/09_6x10_opening_front.jpg" alt=""></a>
	<figcaption>Front clip location.</figcaption>
</figure>

<figure class="half center">
	<a href="/images/FREKVENS/10_6x10_guts.jpg"><img src="/images/FREKVENS/10_6x10_guts.jpg" alt=""></a>
	<figcaption>It's got guts.</figcaption>
</figure>

<figure class="half center">
	<a href="/images/FREKVENS/11_6x10_closer_look.jpg"><img src="/images/FREKVENS/11_6x10_closer_look.jpg" alt=""></a>
	<figcaption>A closer look.</figcaption>
</figure>

<figure class="half center">
	<a href="/images/FREKVENS/12_6x10_closeup_0.jpg"><img src="/images/FREKVENS/12_6x10_closeup_0.jpg" alt=""></a>
	<figcaption>Closeup 0.</figcaption>
</figure>

<figure class="half center">
	<a href="/images/FREKVENS/13_6x10_closeup_1.jpg"><img src="/images/FREKVENS/13_6x10_closeup_1.jpg" alt=""></a>
	<figcaption>Closeup 1.</figcaption>
</figure>

<figure class="half center">
	<a href="/images/FREKVENS/14_6x10_closeup_2.jpg"><img src="/images/FREKVENS/14_6x10_closeup_2.jpg" alt=""></a>
	<figcaption>Closeup 2.</figcaption>
</figure>

<figure class="half center">
	<a href="/images/FREKVENS/15_6x10_closeup_3.jpg"><img src="/images/FREKVENS/15_6x10_closeup_3.jpg" alt=""></a>
	<figcaption>Closeup 3.</figcaption>
</figure>

<figure class="half center">
	<a href="/images/FREKVENS/16_6x10_activities_0.jpg"><img src="/images/FREKVENS/16_6x10_activities_0.jpg" alt=""></a>
	<figcaption>Room for activities?</figcaption>
</figure>

<figure class="half center">
	<a href="/images/FREKVENS/17_6x10_activities_1.jpg"><img src="/images/FREKVENS/17_6x10_activities_1.jpg" alt=""></a>
	<figcaption>Tiny activities, I guess...</figcaption>
</figure>

<figure class="half center">
	<a href="/images/FREKVENS/18_6x10_activities_2.jpg"><img src="/images/FREKVENS/18_6x10_activities_2.jpg" alt=""></a>
	<figcaption>Another view.</figcaption>
</figure>

<figure class="half center">
	<a href="/images/FREKVENS/19_6x10_activities_3.jpg"><img src="/images/FREKVENS/19_6x10_activities_3.jpg" alt=""></a>
	<figcaption>The end!</figcaption>
</figure>

