# OceaniMusica
## Layesta visual charter
---
Hi, you're early! This is the GitHub repo for OceaniMusica. Everything's still in the R&D stage, so there's not much to look at. If you want to see some of what I'm tinkering with, there should be other branches to look at. None of them have anything concrete yet, though.

OceaniMusica will be a visual charter for Layesta. It will focus on using cross-platform libraries, that way it can be ported to any major OS. That being said, OceaniMusica will be primarily developed as a \*nix application. But I won't let that get in the way of letting it run smoothly on other OSs as well!

OceaniMusica's development will be done primarily in C++. At this time, no other languages are planned on being used for any part. Note that this does not mean C libraries won't be included.

POSIX standards will be followed wherever applicable, except in cases where they might do more bad than good. For example, Windows isn't exactly POSIX friendly, so some areas may need to abandon POSIX when compiled on Windows. GNU extensions may also be used from time to time. 

OceaniMusica's core functionality will be a bit simpler and lightweight. That way, even low-end devices can run it. It should be possible to tweak some performance options to take advantage of more powerful hardware. Additional functionality will also be possible using a plugin system. The details of this plugin system are still being worked out.

Feedback and support will link back to this repo, at least at the beginning. I do want to get a better feedback system; I'd like to be able to tell how many users might want a feature or be experiencing a bug without making them all sign up for a GitHub account and write a comment. 

...But all of this is for the future. For now, I'm just going to mess around and get a feel for how I'm going to start this. Once the direction of OceaniMusica has been decided on, and I know more about how to do this, I'll write up the proper stuff and start development.
