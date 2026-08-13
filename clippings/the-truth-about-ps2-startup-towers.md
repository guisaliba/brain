---
title: "The truth about the towers on the menu startup"
source: "https://www.reddit.com/r/ps2/comments/1am3p4u/the_truth_about_the_towers_on_the_menu_startup/?solution=35903f13e59b873335903f13e59b8733&js_challenge=1&token=7afd7253fec22262ff1c52b1703fe9ec4533c176d172c25e55349b1cb0e08a9a&jsc_orig_r="
author:
  - "[[WearyAd1849]]"
published: 2024-02-08
created: 2026-08-12
description: "Seems like most of you don't know this. But the towers are not calculated based on the contents of the memory card. The towers ar"
tags:
  - "clippings"
---
Seems like most of you don't know this. But the towers are not calculated based on the contents of the memory card.

The towers are calculated by parsing the contents of a game play history file that the console updates every time you run a ps2 game, a movie or a program via HDD-OSD/PSBBN.

This history file is stored on the "Your System Configuration" icon you see on the browser. And it can actually be used to know Wich games you played on the past if you still own your old MCs.

This history file records the game ID, and how many times it was launched. With this data, the menu calculates the amount of towers and height.

If you have wLaunchELF, this history file will be found inside one of the following locations:

- `mc?:/BADATA-SYSTEM/`: America, Korea, Hong Kong and Taiwan PS2s
- `mc?:/BCDATA-SYSTEM/`: Chinese PS2
- `mc?:/BIDATA-SYSTEM/`: Japanese PS2
- `mc?:/BEDATA-SYSTEM/`: PAL PS2 (Europe, England, Russia and Oceanía)

Read more

---

## Comments

> **GamingGems** · [2024-02-08](https://reddit.com/r/ps2/comments/1am3p4u/comment/kpj6x1h/) · 23 points
> 
> Damn. This is probably the most pervasive PS2 myth. I remember just a couple days ago someone posted a startup screen with all towers at max height and the comments were asking how they filled up their memory card to capacity.
> 
> Can you cite a source for this?
> 
> > **WearyAd1849** · [2024-02-08](https://reddit.com/r/ps2/comments/1am3p4u/comment/kpjakgc/) · 19 points
> > 
> > > Can you cite a source for this?
> > 
> > You have 3 options:
> > 
> > 1. extract OSDSYS program from PS2 boot ROM and reverse engineer it.
> > 2. look at OPL source code for handling the history file ([https://github.com/ps2homebrew/Open-PS2-Loader/blob/master/src/OSDHistory.c](https://github.com/ps2homebrew/Open-PS2-Loader/blob/master/src/OSDHistory.c) and [https://github.com/ps2homebrew/Open-PS2-Loader/blob/master/include/OSDHistory.h](https://github.com/ps2homebrew/Open-PS2-Loader/blob/master/include/OSDHistory.h))
> > 3. do some tests on emulator to confirm this (run several games without saving progress and see the towers appear, then delete the Your System Configuration icon and see them gone)

> **salduchi1785** · [2025-12-29](https://reddit.com/r/ps2/comments/1am3p4u/comment/nwlu791/) · 1 points
> 
> Do ps1 games and DVD’s add towers to the startup? Or is it only ps2 games?
> 
> > **WearyAd1849** · [2025-12-29](https://reddit.com/r/ps2/comments/1am3p4u/comment/nwlywed/) · 3 points
> > 
> > PS1 games, I don't know
> > 
> > Movies: yes, but all the movies count into the same Tower, identified as `DVDVIDEO` on the history file
> > 
> > > **salduchi1785** · [2026-01-05](https://reddit.com/r/ps2/comments/1am3p4u/comment/nxw6n7q/) · 2 points
> > > 
> > > Just a little update. PS1 games DO make towers on the startup screen.
> > > 
> > > **salduchi1785** · [2026-01-02](https://reddit.com/r/ps2/comments/1am3p4u/comment/nx6cvbz/) · 1 points
> > > 
> > > I’ve watched a few movies on my TV just to test it out. I don’t see any towers for the movies, unless they are in a spot I can’t see very well like the corner.
> > > 
> > > I’ve played two ps2 games and watched three movies and I only have two towers
> > > 
> > > Ps1 games I haven’t tried yet but I’m curious about it
> > > 
> > > **JustSomebody56** · [2026-05-01](https://reddit.com/r/ps2/comments/1am3p4u/comment/ojeflt7/) · 1 points
> > > 
> > >  Sorry for having necrocommented, but I need to ask:
> > > 
> > > What else does the your configuration data do?

> **Optimal\_Emphasis\_952** · [2026-01-11](https://reddit.com/r/ps2/comments/1am3p4u/comment/nyzcao0/) · 2 points
> 
> i play games on opl i have like 15 saves but only 1 tower appear please i need help

> **\[deleted\]** · [2024-02-08](https://reddit.com/r/ps2/comments/1am3p4u/comment/kpjq7pi/) · 3 points
> 
> > The towers are calculated by parsing the contents of a game play history file that the console updates every time you run a ps2 game, a movie or a program via HDD-OSD/PSBBN.
> 
> Hence why I wrote on that other post: "Do you own every NTSC-U game??? WTF."
> 
> > This history file is stored on the "Your System Configuration" icon you see on the browser. And it can actually be used to know Wich games you played on the past if you still own your old MCs.
> 
> This however, I did not know specifically. I understood how it worked, but didn't know where it was kept and this kind of makes me wish I had my original memory cards back from 2009.

> **AutoModerator** · [2024-02-08](https://reddit.com/r/ps2/comments/1am3p4u/comment/kpiypdq/) · 1 points
> 
> Hello [u/WearyAd1849](https://www.reddit.com/user/WearyAd1849/) and thank you for your submission on [r/ps2](https://www.reddit.com/r/ps2/), our subreddit rules have updated recently so please make sure your post is not in violation and is in the appropriate place. All tech support questions should go into the [Tech Support Megathread](https://new.reddit.com/r/ps2/about/sticky?num=2). It can be found stickied on the front page of [r/ps2](https://www.reddit.com/r/ps2/).
> 
> *I am a bot, and this action was performed automatically. Please* [*contact the moderators of this subreddit*](https://www.reddit.com/message/compose/?to=/r/ps2) *if you have any questions or concerns.*

> **Optimal\_Emphasis\_952** · [2026-01-13](https://reddit.com/r/ps2/comments/1am3p4u/comment/nzbpaaj/) · 1 points
> 
> i studied the towers and i came to say some of your info is wrong. the mem card can hold ONLY 21 game towers example: a tower just appeared, it will shrink until its invisble then it will start growing it will not start growing right after it first spawned. and because it only hold 21 game towers if a game tower reaches MAX height it will generate a new one and so on. since the startup can only hold aprox 120 towers so aprox a single game save will hold about 6-10 towers; hence why if you execute lets say 35 games JUST 1 TIME there will be ONLY 21 towers then lets say on of the game is simposns hit and run. if you execute it 40 times then there wil be about 26 towers.
> 
> > **salduchi1785** · [2026-01-28](https://reddit.com/r/ps2/comments/1am3p4u/comment/o2b0u6c/) · 1 points
> > 
> > I’m confused. So if you play a single game enough times it can eventually generate 21 Towers? Could you fill up the whole PS2 startup screen with just one memory card or would it take multiple memory cards and a multi tap?
> > 
> > > **Optimal\_Emphasis\_952** · [2026-02-01](https://reddit.com/r/ps2/comments/1am3p4u/comment/o2y2bot/) · 2 points
> > > 
> > > ur almost right but actually no. a single game it can generate up to 6 towers. and in the startup if we say example you executed 1000 games in ps2 ONLY 21 towers will appear. so if you execute 21 games = 21 towers execute them all 60 times = 126 towers. baisaclly execute a game 10 times a new tower generate up to 6 towers per game