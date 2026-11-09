---
layout: post
title: Networking strategies for real time games with minimal trust
---

These my thoughts **before** doing any research on the topic (other than playing many online games over the years and noting how they perform), because I don't want to be influenced by other people's designs too much.  It's quite likely that some of my ideas are wrong, or else they are right but exist already in the literature with better names and better implementations.

## 0 Pre-requisites
UDP is a protocol for sending packets of data over the internet.  The disadvantages of it are: size of each packet is limited, packets may be dropped if the Internet is congested, or even delivered in the wrong order.  However it is fast.  The alternative is TCP which guarantees delivery but increases latency.  Traditionally UDP has always been preferred for action games, although over a good connection TCP may now be fast enough.

## 1 Dumb terminals
The client sends all input to the server.  The server sends back the game output, e.g. Steamlink video stream, Telnet MUD.
  
Issues:

* encoding video stream and rendering graphics needs lots of power on the server,
* there is latency both directions and also in the encoding/decoding. 
* a buffer is necessary to avoid packet jitter, but the buffer adds more latency.

## 2 Dumb clients
(Improvement of 1.)

The client sends all input to the server.  The server sends back a complete dump of the gamestate. The client runs the game engine locally and used it to draw the output. 

 Issues:

* latency again, jitter again,
* bandwidth requirements can be substantial if the gamestate is large.

## 3a Smart clients
(Optimization of 2)

The client sends all input to the server.  The server sends back a complete dump of the gamestate.  However it doesn't need to do it every frame, because the client runs its own physics simulation in between.  If an object is moving it will continue to move, etc.  When the next dump from the server arrives it may glitch if it moved in a different direction, but this allows the server tick rate to not be linked to the framerate.

Issues:

If the server is running on a player's machine then that player will have lower latency and have an advantage.  The only solution to this, if you care about a fair game, is to add artificial delay to the player's input.

## 3b Diffs
(Optimization of 2)

The server only sends a complete dump occasionally.  In between it just sends diffs.  So that would be just the objects that have changed. this was very important in making games possible over dial up modems, but nowadays in most cases it's just an optimization to reduce your bandwidth costs.

Issues

If you drop any packets (or receive out of order, which might as well be the same thing) then your gamestate is wrong until the next full dump arrives. To work around this people implemented requests for retransmission of dropped packets, but at some point you have to wonder if they are just re-implementing TCP on top of UDP. And dropped packets really shouldn't be common on modern ISP connections. 

Another idea is to assume there will be packet drops and transmit every packet twice. Wastes bandwidth but perhaps saves time (latency). 

## 4 Smarter clients

(Optimization of 3).

If the changes in the objects are entirely predictable, like gravity acting on a projectile, the client can continue to apply them in its own simulation.  Only the creation and destruction of the projectiles needs to be sent.  Thus you save more bandwidth, but if you drop one of these packets you are even more fucked, so you might want to more strongly consider doing retransmission.

## 5 Predictive clients

(Improvement of 4.)

The client can predict what its local player is going to do with complete accuracy - it has his input.  Therefore it can apply them to the simulation immediately, eliminating the round trip latency to the server and back.  So now the client is the apparently the authoritative source for what the player is doing and the server doesn't need to send the player's position anymore, for example.  The problem is now the gamestate of the client and server are not in sync.  E.g. the position of the player is slightly ahead on the client.  Does this matter?

Maybe not.  Collisions with the background will not be any different.  Collisions with sprites might occasionally be different, so you have to do all collision detection on the server only.  The issue with this is that it may result in glitches, where what looks like a hit to the client is actually a miss.

Supposedly it is also possible to predict what other players will do before they do it, but I'm not sure how.

## 6a Trusted clients
(Improvement of 5, possibly)

One way to reduce these glitches is to trust the client.  For certain events that are mostly likely to be annoying glitches, like the player being shot, you make the client the authoritative source.  If the client shows the player got hit, then it informs the server, and he did.  The problem is that it is then possible to cheat using a hacked client that lies to the server.

## 6b Glitch merging
(Improvement of 5, possibly)

Another way is when you receive a gamestate dump that differs significantly from the local gamestate, you don't apply it immediately.  Instead you generate a new gamestate that is a merger somewhere between the incorrect local state and the correct state.  The problem with this is if you got out of sync  once you probably will again, so the local game might never catch up to the 'real' state.  So you've effectively introduced a permanent increase in latency.  I don't know if this method works, I have not tested it myself.

## 6c Rollback
(Improvement of 5)
This also involves trusting the client, but not to generate events.  The only thing server trusts is the input from the client.  However, the client is trusted to tell the server about input that happened in the past.  Each input has a timestamp on it.  When the server receives this it rolls back the simulation to the time of the input and then re-runs the simulation with the input applied.

I guess you wouldn't want to rollback on every frame so you'd want to buffer the incoming inputs on the server.  Rollback is then only necessary if the buffer empties and you have to generate an update that is missing the input of a player.  This method seems to be preferred for fighting games where the order of the inputs received is very important - did the player block 1 frame before the attack or 1 frame after it.  But they don't all use it, and I'm not sure if it's helpful for other genres.  It doesn't eliminate glitches after all.  Also not sure if it can be applied to a game that is not fixed frame rate and the time step is variable.

## ?Lockstep simulation?

(Alternative to 5?)

If our client gets out of sync with the server it seems inevitable there will be glitches. So how about we keep them locked together? If the client doesn't receive an updated gamestate it waits for a retransmission and freezes until one is received. If the server is awaiting input from any player it does the same. (So there is input buffer needed on server). Any dropped or delayed packets won't cause glitches, the game will just freeze. In that sense it's fair to all players, but it means one player with a crappy connection will slow down the game for everyone. 

<strike>
## ?Slow motion?
If your buffer runs out with any of these techniques then you have a problem.  You could freeze until the next frame arrives, but then you don't have much of a buffer against jitter any more.  So you could display 'buffering' like a youtube video and freeze until the buffer fills to full capacity, but then you have a big pause.  So I'm wondering if you could instead fake the game timestep while the buffer is filling.  If your buffer is full then the game runs normally.  If it starts to empty then you make the game run in slow motion until it fills again.  Usually this should be unnoticeable to the player, but it should increase the effect as the buffer empties, until the game completely freezes at 0.
</strike>

