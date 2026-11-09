---
layout: post
title: Twin-stick shooter controls
---

Currently <a href="http://electronstudio.co.uk/uniblaster_mod/">UniBlaster</a> (the main engine of
<a href="http://retrowar.net">RetroWar</a>) supports four different games / character types. 
They are 
similar
 in many ways, 
but the controls vary slightly.

* **Droids** use the right stick to aim, and automatically shoot a stream of low powered bullets (**A**)
* **Tanks** use the right stick to aim, but require the button to pressed to shoot a single high powered projectile 
(**B**)
* **Ships** cannot aim, fire straight forward when the button is pressed (**C**)
* **BombBots** have no gun so cannot aim, drop bombs when button is pressed (**C**)

I've been thinking how to create a more general abstraction of these differences.

Instead of one weapon, each character would have three weapon slots:

* **A** fires when right stick is moved, unless button is depressed
* **B** fires when right stick is moved and button is depressed
* **C** fires when right stick is neutral and button is depressed

This would allow characters to carry multiple weapons and use all three without any switching and only needing one 
fire button.  

Possible uses:

* The current shooting-type **A/B** characters could gain a close combat **C** weapon.
* Player has a choice between firing a stream of low power bullets, or one high power bullet that will take time to 
reload.
(Also can make reload not begin until player has finished aiming - see <a href="http://www.cross-code.com/">CrossCode</a> for example of this.)
* Player could be given a choice between firing low power bullets, or pressing the button and firing high power bullets
 but
reducing his speed, perhaps to zero. (Need to add speed reduction option to weapons)
* Player could be given a choice between shooting and dropping bombs, depending on whether he moves right stick.
* An **A** type weapon that does no damage, but merely assists in getting the aim right before the **B** type
weapon is fired.
* A **B** type weapon that doesn't fire when the button is pressed, but when it is released.  Thus holding the button
down does nothing, so fire rate entirely depends on how quickly the button is mashed.  The amount of time the button
is held before release could determine how charged up the weapon is.  Why not fully charge every shot?  Because 
charging reduces
 your movement speed.

Finally, I've been thinking about how RetroWar could be played on actual 8-bit joysticks.  Currently 8-way d-pad 
movement is supported in all games as a virtual stick, (although it puts you at a disadvantage in most of them that 
aren't grid based.) 

But then how to aim when there is no second stick for aiming?  You could just fire in whatever direction the sprite
is facing when the button is pressed.  But that would fire the **C** type weapon, which is likely to be 
non-directional bomb anyway, and leave no way to fire the **A** directional gun.
Games like 
Paradroid handled this by requiring
you to move a bit before pressing fire.  So the virtual input would create a second stick pointing in the same direction
as the real left stick when you press the button with no input from any right stick.  Many games also had a locking
mechanic, so once you started shooting you held down the button to lock the firing direction while you could move
in a different direction.  Not sure how that could work in my scheme.

