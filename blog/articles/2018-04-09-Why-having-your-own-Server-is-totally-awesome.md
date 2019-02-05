## Why having your own Server is totally awesome

04/09/2018

Around 2015-2016 I was getting more and more involved in webdevelopment. Before that my coding revolved mostly about some Batch scripting or Automation scripts with AHK. Nothing fancy and barely over 100 lines each. Having made my first *somewhat* good looking website at that time, I wanted to made it available to the public eye. At first I used some weird free webhosting. A couple weeks later, a friend of mine recommended that I rent a cheap Linux VPS. Things changed after that. Drastically. Having my own server instead of just that mediocre webhosting introduced me to a whole lot of things that I learned to love in the following years. Including Linux administration and the whole world of selfhosted software. Especially selfhosting is so useful, I can't image going back now. To make it more clear, here are a couple things I do or at one point did with my server:

- Own webserver. Serving any content I like, using any software I like. (Try convincing your shared hoster to switch to a different DBMS). Also updating ASAP instead of weeks later.
- Hosting my [ownCloud](https://owncloud.org/) to backup and share files from. Kinda like dropbox. Files are encrypted as well.
- A small reddit and a telegram bot.
- My own instance of [gitlab](https://about.gitlab.com/)
- A script to idle hours on my Steam alt account, which I build my [own Webinterface](https://github.com/p410n3/SteamHourBoostWebInterface) for.
- NMap, WhatWeb and other interesting security tools from the [Kali](https://www.kali.org/) linux repos, to launch penetration tests on my own server and sites. (My laptop was too slow)
- Used it as an CnC back when I was fiddling with AV evasion and [Metasploit](https://www.metasploit.com/).
- Use it as an VPN.
- An [PHP based proxy](https://github.com/joshdick/miniProxy). For some reason email websites are blacklisted at my school, so I use an PHP proxy to connect through my webserver, bypassing the blacklist.
- This blog obviously.
- An image hoster for sharing my screenshots. Instead of having them uploaded to Gyazo or imgur. (Services I can't control) They are uploaded to my own server using shareX and [THIS](https://github.com/Quietess/sharex-upload-script) script.
- Converting of big files, so I can still use my PC while my server is at 100% CPU rendering things.

I probably have forgotten a couple things too, but these are enough to hopefully show that selfhosting can be really awesome. Especially people who care a bit about their privacy will see great value from having their own server. But hey, it's too expensive right? No. Not at all. Many People seem to think that renting a server means to rent a full machine in a data centre. But we live in the age of virtualization, so buying a virtual server is the way to go. My first Server costed 1.50€ / month and I hosted 2 small websites, an owncloud instance and an TeamSpeak Server there. 1 vCore and 512 mb ram are plenty for that, and I only upgraded my package once I started working with server side programming and MetaSploit more. These Services can be pretty demanding at times. Learning to set up an whole Webserver Stack on my own and how to properly use Linux from the Terminal was not only fun, it's a skillset I use nearly every day at my current Job. So if you want to get into full-Stack web-development specifically, this will get you started. If you are living near Germany I recommend [dyn-box.de](https://dyn-box.de/), I am a Customer there for 2 years now. Otherwise [OVH](https://www.ovh.de/) is always a safe bet. (This article is not sponsored by anyone btw) Now, go out and have some fun with you Server!
