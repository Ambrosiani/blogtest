---
layout: post
title:  "Levels of Open Source, Revisited"
date:   2017-09-01 12:00:00 +0100
tags: [Open Source]
author: Aron Ambrosiani
---

In a [previous blog post](http://aron.ambrosiani.se/2016/04/11/open-source-in-museums-now-what/), I tried to characterize four levels of open source usage in the museum sector. I’d like to return to these levels, adding examples from my own workplace, the Nordic Museum.

# 1) using open source

*These museums use open source projects (probably WordPress or Drupal, maybe some Javascript frameworks as well), but treat them as a regular vendor-supplied application – except that they’re for free.*

At the Nordic Museum, we run our websites using Drupal and Wordpress, as well as using open Javascript frameworks like Leaflet (for interactive maps) and React Native (for our audio guide app) in different projects. Still, most of the software used at the museum is proprietary.

# 2) using & writing open source

*These museums use open source applications and projects, and also have in-house technologists that actually write their own code to solve some problems. They share their work even though the code is tailored to their own specific setting. Why not put it on Github though?*

For the recent exhibition Nordic Light, the museum made an interactive children’s experience called "The Journey of Light". The backend was a three part setup: 

1. Raspberry Pis in the exhibition detect kids using RFID-modded "magic candles", by running a python script connected to a PN532 RFID sensor. The detected RFID chips are sent using http requests to…
2. a "server" Raspberry Pi running a Node app. Using the requests sent from the other Raspberry Pis, the server keeps track of sessions while also passing on on/off commands to…
3. a proprietary media controller (Medialon) which activates light effects in the exhibition based on the kids’ interactions.

All these three parts were developed by outside consultants (Interaktiva rum, Earthpeople & Kreativ teknik). Parts 1 ([nfc2server](https://github.com/NordicMuseum/nfc2server)) and 2 ([Ljusresan](https://github.com/NordicMuseum/Ljusresan)) have been released as open source on the Nordic Museum Github account. Although they are tailored to fit the Nordic Museum setup, both projects could be used by other museums either by adapting the code or using it as a learning resource.

# 3) using & writing & contributing to open source

*These museums not only put their own stuff on Github, but are involved in other open source projects too. They contribute with plugins for their open source CMS and help solve general problems, not only those that are specific to the institution’s needs.*

There are a few Drupal & Wordpress modules written to solve specific problems at the Nordic Museum, but they have not been released as open source.

# 4) using & writing & contributing to & collaborating on open source

*These museums combine forces with other museums on open source projects that fulfill overlapping needs. Working together, they can solve more complicated problems not only for the participating institutions but for other institutions as well.*

During the spring and early summer, we had the opportunity to cooperate with the Innovation Studio at the Carnegie Museums in Pittsburgh. Instead of making our own audio guide app from scratch or putting our content into a proprietary app, we adapted the existing Warhol Out Loud app to fit the Nordic Museum’s needs. The lessons learned will be discussed at the upcoming MCN conference in Pittsburgh in November, in a session named "[Open Source Reality Check](https://conference.mcn.edu/profile.cfm?profile_name=session&master_key=51947569-0816-D127-AB51-23ABF63F3198&page_key=&xtemplate&userLGNKEY=0)".

# Now What?

Do you agree with this blunt classification? How would you characterize your museum’s open source efforts? How do we move from solving problems in a specific way to solving them in a general way applicable to other museums as well?