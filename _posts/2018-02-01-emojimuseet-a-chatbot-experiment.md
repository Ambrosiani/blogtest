---
layout: post
title:  "Emojimuseet – a chatbot experiment"
date:   2018-02-01 12:00:00 +0100
tags: [Open Source, Chatbots, Emoji, Javascript, Collections]
author: Aron Ambrosiani
---
Back in October 2017, I soft-launched a Swedish clone of the lovely Twitter chatbot [NYPL Emoji Bot](https://twitter.com/nyplemoji). Basically it is a node app listening to Twitter mentions aimed at [@Emojimuseet](https://twitter.com/emojimuseet) which 1) checks if there’s an emoji in the tweet, and if there is 2) replies with a URL pulled from a static JSON file. There’s also a ”status” script that tweets a random emoji with matching URL which can be run by a cron job at regular intervals.

The [code for the NYPL Emoji bot](https://github.com/lolibrarian/NYPL-Emoji-Bot) is open source and available on Github, so there were only a few steps to get it up and running:

1. Fork the project & update the .env file with Twitter credentials
2. Replace the NYPL urls with new links to Swedish museum collections (work in progress – see below)
3. Find a server to host the app. Luckily the Nordic Museum already has an excellent and flexible hosting provider (hi [Cloudnet](https://www.cloudnet.se)!) who setup a PM2 process for me to keep the app running.

I added a bunch of emojis and invited museum colleagues around Sweden to contribute with emoji ideas from their own collections. Right now, after lots & lots of very serious emoji research at multiple institutions, around 800 emojis have one or more matching urls from five different sources: [Digitalt museum](https://digitaltmuseum.se) (a joint site for more than 50 Swedish museums), [Nationalmuseum](http://collection.nationalmuseum.se/eMP/eMuseumPlus), [Världskulturmuseerna](http://www.varldskulturmuseerna.se/forskning-samlingar/sok-i-samlingarna/), [Stockholmskällan](https://stockholmskallan.stockholm.se) and [Spårvägsmuseet](http://sparvagsmuseet.sl.se).

As a side project during January 2018, I wanted to find out if I could get the bot running on Facebook as well. There are a few node modules available that provide a middleman for the Facebook Messenger API, and decided on [messenger-bot](https://github.com/remixz/messenger-bot). The code is horribly written (since I never quite get the hang of proper object-oriented programming) but hey, it works. Again I needed help from Cloudnet to get the server-side connection working (in particular, Facebook Messenger requires a https connection) but the app is up and running and available at facebook.com/emojimuseet. One snag in the app review process was that the fields for example queries and responses actually couldn’t handle emojis, confusing both app reviewers and myself until I figured out what was going on.

Try out the chatbot on [Twitter](https://twitter.com/emojimuseet) or [Facebook](https://www.facebook.com/Emojimuseet/)! The code is available on [Github](https://github.com/Ambrosiani/Emojimuseet).