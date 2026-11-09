---
layout: post
title: Should you use a physics engine in your game?
---
In the real world, (almost) every object moves according to a set of laws known as Newtonian physics. If you want the virtual world of your game to feel realistic then it must implement the same laws. The easiest way to do this is to use a third party library such as Box2d. It will save you time and will probably be more accurate and efficient than your own physics code. However there are some cases that justify doing it yourself. 

* You want your game to behave like some classic game which did not use any realistic physics. 

* The physics of your game are Newtonian but the situations are very simple so you only need a small subset of the features of Box2d. 

* You want some Newtonian physics but you also want some physics that are unique to your game. 

Let's see how Newtonian some common game control systems are. 

1. Constant velocity Movement (Space Invaders gun). You push left or right and it moves that way at constant velocity. You stop pushing and it immediately stops. 

2. Variable velocity Movement. As above but you can vary the velocity depending how hard you push on the analogue stick. Acceleration to the selected velocity is still instant so non Newtonian. Works for 2d as well as 1d movement. 

3. Newtonian 4 thruster. (Space taxi). Proper Newtonian physics with the limitation that your object is a square that cannot rotate. It has 4 fixed thrusters that can accelerate it up, down, left or right. Easy to implement because each thruster corresponds perfectly to an axis in two dimensions, and the screen is 2d, and joystick input is 2d. Gravity can also be modelled as a downward acceleration. Rather difficult for the player. Realistically in a vacuum speeds would be unlimited, which is problematic, and in atmosphere speeds would be limited by frictional forces, which you may not want to bother with, so you could just cut off thrust at a maximum velocity. 

4. Auto stabilized 4 thruster. As above, but player does not have direct control of the thrusters. Instead player uses analogue stick to input the desired velocity and thrusters are automatically fired to achieve this and automatically cut out as soon as it is achieved. Works well for 1d too. 

5. Brakes. As above, but the thrusters become more powerful when reducing velocity towards zero. This is realistic for an object in contact with the ground which could apply friction to slow down. 

6. Fast turns. Even with powerful breaks, a 1d character can feel sluggish when reversing direction. Probably because a 3d character could reverse direction without breaking simply by sharply steering. To emulate this we could skip velocity straight from +X to -x without going through zero. 
