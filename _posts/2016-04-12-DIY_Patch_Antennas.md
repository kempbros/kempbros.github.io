---
layout: post
title: DIY patch antennas for longer range FPV
description:
modified: 2016-04-12
tags: [patch anntenna rf electromagnetic radiation spectrum fpv EAGLE script scr]
categories: [Antennas]
excerpt: Thinking about using a patch antenna with your FPV setup? Well, you might want to read this...
---

## Rubber duck vs Patch:
When first getting into the wonderful world of FPV (first person view) you often start off with two monopole “rubber duck” antennas that are provided with your setup. These antennas are very inexpensive to manufacture as they often are made out of the coaxial wire itself with a small bit of the shielding removed at the end, forming the antenna. What you will discover is that these antennas produce an omnidirectional signal pattern roughly in the shape of a toroid (kind of like a doughnut) and have a signal that is linearly polarized. In Layman's terms, you have to have your antenna receive (Rx) in the same orientation as your transmitter (Tx) in order to get the clearest signal. While your Rx is sensitive enough to not really care about antenna orientation when your Tx is close by, the farther away you get, or the more obstacles you have between you and your Tx, the more loss you have.

<figure class="half center">
	<a href="http://www.cisco.com/c/dam/en/us/products/collateral/wireless/aironet-antennas-accessories/prod_white_paper0900aecd806a1a3e.doc/_jcr_content/renditions/0900aecd806a1a3e_null_null_null_08_07_07-04.jpg"><img src="http://www.cisco.com/c/dam/en/us/products/collateral/wireless/aironet-antennas-accessories/prod_white_paper0900aecd806a1a3e.doc/_jcr_content/renditions/0900aecd806a1a3e_null_null_null_08_07_07-04.jpg" alt=""></a>
	<figcaption>Dipole antenna pattern (similar to monopole) - Antenna Patterns and Their Meaning, Cisco 2007</figcaption>
</figure>
	
Now, if you take all of that RF energy and point it in one direction (directional), rather than in all directions (omnidirectional) you can extend the range or permeability of your setup. A good analogy to this effect is talking through a plastic megaphone, or using one to listen through. You don’t change how much energy is used to create your voice, you just change how it's transmitted.

<figure class="half center">
	<a href="http://www.cisco.com/c/dam/en/us/products/collateral/wireless/aironet-antennas-accessories/prod_white_paper0900aecd806a1a3e.doc/_jcr_content/renditions/0900aecd806a1a3e_null_null_null_08_07_07-07.jpg"><img src="http://www.cisco.com/c/dam/en/us/products/collateral/wireless/aironet-antennas-accessories/prod_white_paper0900aecd806a1a3e.doc/_jcr_content/renditions/0900aecd806a1a3e_null_null_null_08_07_07-07.jpg" alt=""></a>
	<figcaption>Patch antenna pattern (similar to monopole) - Antenna Patterns and Their Meaning, Cisco 2007</figcaption>
</figure>

So why is a patch antenna the best for FPV you ask? ... Well it’s not necessarily the BEST. There will be situations where you are flying and the antenna gets pointed away from you and you lose signal altogether. Trust us...we tried. So all in all, its best to use an omnidirectional antenna on your Tx side, a patch on your Rx and simply reposition the antenna by moving your head to optimize the signal. The big bonus about using a patch antenna is that they are quite easy to make and the results are pretty stunning. What I mean by this is that because the patch antenna “focuses” the signal more along one axis than the other, there are situations where you lose signal completely if you do not have the antennas aligned. This fact limits the usefulness of a patch antenna on the Tx side since you cannot really control it's orientation. Enter polarization.

## Antenna polarization:
The monopole antenna we discussed earlier produces a waveform that is only on one axis, or linearly polarized (LP). You will notice the effect of this quite clearly with your RC Tx Rx where you can improve the range of your Tx simply by changing the orientation of your transmitter until the antennas align. An alternative to this linear polarization is to add a small instability to the means in which the signal is generated and the result is a waveform that travels in a circular pattern, or circularly polarized. This polarization can be clockwise (right hand - RHCP) or counterclockwise (left hand - LHCP) and is determined by the design of the antenna. For best results, you will want to use a Tx and Rx antenna with like polarization. Luckily for you, our calculator can produce all three LP, RHCP and LHCP.

<figure class="half center">
	<a href="http://hyperphysics.phy-astr.gsu.edu/hbase/phyopt/imgpho/polcls.gif"><img src="http://hyperphysics.phy-astr.gsu.edu/hbase/phyopt/imgpho/polcls.gif" alt=""></a>
	<figcaption>Classification of Polarization - hyperphysics.phy-ast-gsu.edu</figcaption>
</figure>

## Patch antenna design:
While patch antennas are easy to make and have very low physical profiles, their design is very sensitive to the materials used, polarity required and location of the signal feed. Rather than leave the design of these antennas up to the manufacturers we decided to create a calculator and make our own. Because, you know, buying things is for suckers. You can now make one too by simply inputting your frequency, dielectric constant, material thickness and ground plane scale factor into our calculator and watch the magic happen.

<figure class="half center">
	<img src="/images/FPVPatch.jpg" alt="">
	<figcaption>Homebrew patch ready for testing</figcaption>
</figure>

Ready to build your own? Awesome. We here at KempBros have done all of the hard work for you and created a complex patch antenna calculator for all of your coaxial-fed patch antenna needs. Just hit "Generate" to design your frequency specific LP or CP antenna. Enjoy!

<a href="http://kempbros.github.io/antennas/Patch_Antenna_Generator/" align="center"></a>

## References:
<a href="http://www.everythingrf.com/rf-calculators/microstrip-patch-antenna-calculator>"></a>
<a href="https://www.pasternack.com/t-calculator-microstrip-ant.aspx"></a>
<a href="http://ijates.com/images/short_pdf/1408805121_P378-384.pdf"></a>
<a href="http://www.ijecse.org/wp-content/uploads/2012/06/Volume-3Number-2PP-159-166x.pdf"></a>
<a href="http://ijettjournal.org/volume-4/issue-4/IJETT-V4I4P340.pdf"></a>
