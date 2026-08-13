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
