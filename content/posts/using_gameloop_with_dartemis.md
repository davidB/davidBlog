---
title: "Using game_loop with dartemis"
description": ""
date: "2013-09-18"
categories: ["articles"]
tags: [ "vdrones", "lang/dart"]
---
Today, I replaced `requestAnimationFrame` + my own TimeInfo class by [game_loop][], you can see the [commit on github](https://github.com/davidB/vdrones/commit/2bd69af25ee739d5e2cd94b6dbcdef08d33f773f).

So how to use [game_loop][] with [dartemis][]:

{{% gist id="7181741" file="dartemis_game_loop.dart" %}}

Why I moved to [game_loop][] ?

I was happy with my previous solution, but I planned to move when I need some of its features like gamepad support, fullscreen, constant update time, … And today I need (for debug purpose) the easiest feature to implement: a frame counter. I spend more time to introduce [game_loop][] than to implement the frame counter ;-) , but less time than implement it and replace it later.

Currently I didn’t replace the keyboard management by the [game_loop][], may be later.

   [game_loop]: https://github.com/johnmccutchan/game_loop
   [dartemis]: https://github.com/denniskaselow/dartemis