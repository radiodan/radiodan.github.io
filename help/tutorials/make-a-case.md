---
layout: page
title:  "Make a case for a Raspberry Pi Radio"
---

Make a case for a Raspberry Pi Radio
===

## [laser cutter](#laser) | [cardboard and scissors](#cardboard)

<p class="todo">Remove [old instructions](https://github.com/radiodan/project/blob/master/docs/case_construction.md)</p>

This guide describes how to make a case, providing templates for a laser cutter and for a hand-made version in cardboard.

The case is designed (by Victor Johannson) to be something 
that can be changed and adapted to the size of different components.

Here we use a USB soundcard and a 5cm diameter speaker, but we've also 
experimented with versions with cheap miniature speakers instead, though 
in that case you may need to increase the number of corner pieces and 
make the side pieces wider (and the sound won't be as good).

It's also designed to be laser cut in 3mm acrylic or MDF, but we have 
made versions successfully in cardboard, although the button press 
movements mean that the top piece and supporting side bar need to be 
quite stiff ([see below](#cardboard)). 

<a name="laser"></a>

First, [make your Raspberry Pi radio](basic-pi-radio.html).

{% capture laser %}{% include laser-cut-box.md %}{% endcapture %}
  {{ laser | markdownify }}

Next steps
--

You may want to [add some buttons and dials](buttons-and-dials.html)

----

<a name="cardboard"></a>

First, [make your Raspberry Pi radio](basic-pi-radio.html).

{% capture cardboard %}{% include cardboard-box.md %}{% endcapture %}
  {{ cardboard | markdownify }}

Next steps
--

You may want to [add some buttons and dials](buttons-and-dials.html)
