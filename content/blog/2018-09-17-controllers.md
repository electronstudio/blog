---
layout: post
title: Phones as game controllers
---

The <a href="http://www.retrowar.net">game I am working on</a> is a local multi-player party game for up to 16
players.  However not many people have 16 controllers connected to their PC.  So I was thinking about using
phones as additional controllers.

I can think of a couple of different ways to do this:

* Create and publish a native app for Android and iOS.  The PC game runs a server, the app scans for servers on the LAN 
and automatically
connects.  Touch input is sent in UDP packets.  Bonus: server could announce "this is a d-pad game" or "this is a 
twin stick game" and the app could display appropriate input controls.

* Write the app in JavaScript.  Have the game run a webserver, which serves a page containing the app.  Tell players to 
open the IP address of the server in
their mobile browser.  The browser runs the JavaScript app and uses Websockets to send the touch input to the server.

This seems such a simple, useful re-usable project that I would expect it has been done before.  Does anyone know?
If not, is anyone interested in working on it?  It might make a nice little project for a student.
