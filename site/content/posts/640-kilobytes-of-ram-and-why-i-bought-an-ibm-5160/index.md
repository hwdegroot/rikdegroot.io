---
title: "640 kiloBytes of RAM??! and Why I Bought an IBM 5160"
date: 2020-05-19T18:43:42Z
type: post
tags:
    - development
    - vintage-computing
    - ibm-5160
    - lang-en
images:
    - images/og/ibm-5160.png
disqus_identifier: "f355ef2ad8ff0047813f58db28ac801d"
disqus_title: "640 Kilobytes of RAM??! and Why I Bought an IBM 5160"
showComments: false

---

> 640 Kilobytes!!!!1!!1 I shit you not. That is like 10 times the size of Donald Trump's brain.

Recently I was trying to get my son enthousiastic for programming. At the time of writing he is 7 years old and getting interested in all kinds of electronics,
so I thought that getting acquainted with programming would not hurt him. And I like to think of myself as a parent that stimulates his kids, so I used that
as an excuse to look into older computers, because _nostalgics_.

[Show me them footage](#show-me-the-pics)

My kids grew up with LED monitors and TV's and never really saw a real cathode tube, except on the episodes of [Pat & Mat](https://en.wikipedia.org/wiki/Pat_%26_Mat).
I still remember the soft fading sound of of the tv turning off and the graphics vanishing into this thin line.

{{< video "videos/mesmerizing-shutdown.mp4" >}}
Mesmerizing shutdown. The terminal vanishes into a line.
{{< /video >}}

Besides that, I am a fan of clicky keyboards. I have a [DasKeyboard 4C ultimate](https://www.daskeyboard.com/daskeyboard-4C-ultimate/) tenkeyless with Cherry Blue switches and a [4C Profressional](https://www.daskeyboard.com/daskeyboard-4C-tenkeyless-professional/) with brown switches. Sitting at home during the
COVID-19 period, made me google old skool stuff a lot.

So first I laid my eyes on a [IBM Model M2](https://clickykeyboards.com/product/ibm-model-m2-1395300-made-by-ibm-06-30-1993/) and got this pretty cheap on
the dutch eBay. Getting this to work on my modern laptop was not rocket science, but not straight forward either. I warned my collegues
that the quiet days at the office were over. But this also opened up a window into vintage computers and computing. What if I could get a vintage computer, I thought. How awesome would that be?

How cool would it be to program a vintage computer with my collegues, or my kids. With all the speed we get nowadays, who still thinks about the limits of computing power. This will be totally different if you have just a fraction of the memory and chip available.

## IBM 5160 or PC XT

I am from 1983. So I was looking for a computer from that year. IBM was _the company_ in those days for personal computing and when it came to making PC's (I am NOT an apple fan). So I found that IBM produced the [**IBM PC XT**](https://en.wikipedia.org/wiki/IBM_Personal_Computer_XT) in that year. I also found out that you could still get them online for a reasonable price.
Luckliy I was able to lay my hands on one, in a pretty good state. It came with an [IBM Model M](https://clickykeyboards.com/product-category/1986-1989-ibm-model-m-silver-label/) keyboard with the silver label (the PC is from 1986). The sound of that is even better than the `Model M2`.

{{< audio "audio/IBM-model-m-oh-that-clicky-sound.mp3" >}}
Need I say more...
{{< /audio >}}

After introducing my kids to th `DIR` command (it was the only one I was pretty sure about it would work), they wanted to type "words" on the old computer (first success).

## Exiting Vim is hard?

So, I know the `DIR` command. But now what. Let's see what commands are available.

* No tab completion. `TAB` just places the cursor somewhere down the line
* No `HISTORY`. You can repeat the last command by pressing the right-arrow.

**FEEDBACK**

> This is incorrect. You say that you have IBM PC DOS 5. If so, this includes the DOSKEY command. This will give you a command-line history with editing. Just type `dos\doskey` to load it.

For a starters, on `IBM DOS` (version 5.0) there is no `$PATH` (or `%PATH`). The executables are located in `C:\DOS` (or `c:\dos`, because `DOS` don't care about casing). the most executables are located. After a day or two I figured this out, so I finally managed to open my first `BASIC` program. All fine, until I wanted to quit the program. It's not that easy as [exiting `Vim`](https://stackoverflow.com/questions/11828270/how-do-i-exit-the-vim-editor). It took me quite some time googling, until I finally found this [lifesaver](https://stackoverflow.com/questions/44253055/how-can-i-exit-microsoft-gw-basic-ibm-basica-or-other-similar-old-dialects-of).

**FEEDBACK**

> There certainly should be! DOS has 2 configuration files, which live in the root directory of the boot drive (A: or C:). They are called [1] CONFIG.SYS and [2] AUTOEXEC.BAT. In the 2nd, there should be a line:
> `PATH=C:\DOS; C:\`

{{< image "images/basic-startup-screen.jpg" Fit "600x600" >}}
Entering BASIC is peanuts
{{< /image >}}

{{< image "images/cannot-exit-basic.jpg" Fit "600x600" >}}
Stuck in BASIC
{{< /image >}}

{{< video "videos/trying-stuff-in-qbasic.mp4" "letter" >}}
Trying to exit QBASIC. Epic fail
{{< /video >}}

**FEEDBACK**

> That is *not* `QBASIC`; `QBASIC` has a GUI. You were in either `BASICA` or `GWBASIC`. The command to quit is `syst em`, if I remember correctly after 30 years.

So, now I can start a few commands, but getting all available commands is not that straight forward. There is a lot in the `DOS` directory, but there is no scrolling, and the monitor only is 25 lines.

**FEEDBACK**

> Yes there is [scrolling]. Type `dir /p` for page-by-page. `dir /w` gives a wide listing. You can combine these: `dir /w /p`. You can also do `dir | more`

> [the monitor is only 25 lines] This depends on the graphics card. If you have an MDA card, no, 25 lines is all. Try `mode con: lines=43` or `mode con: lines=50`. This will only work on a VGA-compatible card, though, and you will need ANSI.SYS installed, I think.

So figuring out the available commands is using a lot of `DIR *.EXE`'s and `DIR *.COM`'s.

First class fun.

## Show me the pics

Not so long ago I was explaining my collegue (who is using a screensaver), [where a screensaver got its name from](https://en.wikipedia.org/wiki/Screensaver). Back in the days, when we were all running the [pipes](https://www.youtube.com/watch?v=Uzx9ArZ7MUU) so the screen would not {{< censor >}}f*ck up{{< /censor >}}.

But now, sit back and relax...

{{< video "videos/insane-refresh-rate-oldskool-monitor.mp4" >}}
Check this insane refresh rate of the cathode tube. The color of the terminal is magnificent! 😍
{{< /video >}}

{{< video "videos/more-refresh-rate.mp4" "landscape" >}}
And more refresh rate. The mesmerizing fading away of the fonts into the background. Beautiful, just beautiful
{{< /video >}}

{{< video "videos/booting-into-dos.mp4" >}}
🔈 The startup is amazing as well. The sound of the fan, and the nostalgic beep.
{{< /video >}}

{{< video "videos/booting-into-dos-again.mp4" >}}
🔈 One more time. I could loop this forever.
{{< /video >}}

{{< image "images/ibm-dos-edit-dutch.jpg" Fit "600x600" >}}
un DOS tres. The fluorescence is soooo pretty.
{{< /image >}}

{{< image "images/wpview-printer-driver-bat-file.jpg" Fit "600x600" >}}
wppreview, I totally miss the point of this program. But, hey, it's there.
{{< /image >}}

**FEEDBACK**

> It [wppreview] is not part of DOS. Sounds like a WordPerfect preview program for use with mailmerge.

## What next?

So far I had to explain to my son what a `file(name)` and a `command` is (when they were typing "words" the IBM kept returning

```cmd
Bad command or file name
```

So the experience is already educational :)

To be honest, I do not have a clear idea what I am going to do with it next. I will be playing with it for a while like an 8 year old with his trains.
After the [`#stayathome`](https://twitter.com/hashtag/stayathome) is over, hopefully I can take it to the office, so we can start doing real cool things with it.

I will definitely have to up my [`GOTO`](https://www.qb64.org/wiki/GOTO) skills :)

I will start using my Model M2 for work (sorry collegues), for sure. I will have to remap my function key in [`i3`](https://i3wm.org/), because I am currently using the
windows key for this. But the Model M2 does not have one. But I will overcome.

**FEEDBACK**

> It is easy to remap CapsLock to be a “Windows” (Super) key. This is how I use my IBM Model M in Linux. I suggest `xmodmap`.

Besides that, I found this great archive with [manuals](ihttps://archive.org/search.php?query=dos%20ibm) and [bootdisks](http://www.retroarchive.org/dos/disks/) and even [PC DOS 5.02](https://winworldpc.com/download/40c2a543-4218-c39a-11c3-a4e284a2c3a5). Currently I am trying to get a VM up running PC DOS 5.0 (yes, that is possible in [virtualbox](https://www.youtube.com/watch?v=xfjUkJMe_kw))

**FEEDBACK**

> If you are willing to change the DOS version, I suggest DR DOS 3.41. The reason is this: MS/PC DOS 5, 6 & later are designed for 386 memory management. This is impossible on an 8088 chip, and as a result, you will have very little free memory. Many DOS programs won’t work.

> DR-DOS is a better 3rd party clone of DOS, by the company that wrote the original OS (CP/M) that MS-DOS was ripped-off from. The first version is 3.41 (before that it had different names) and it is far more memory-efficient. https://winworldpc.com/product/dr-dos/3x

> But if you want to stay with an IBM original DOS, then IBM developed PC DOS all the way to version 7.1, which supports EIDE hard disks over 8GB, FAT32 and some other nice features. It is a free download.

> I have described how to get it here: https://liam-on-linux.livejournal.com/59703.html

> PC DOS 7 is a bit strange; IBM removed Microsoft’s GUI editor and replaced it with an OS/2-derived one called E, which has a weird UI. IBM also removed GWBASIC and replaced it with the Rexx scripting language.

> Personally, I combine bits of PC-DOS 7.1 with Microsoft’s editor, Microsoft’s diagnostics, Scandisk disk-repair tool and some other bits, but that is more than I can cover in a comment!

> There is a lot you can do to upgrade a 5160 if you wish. Here is a crazy example: https://sites.google.com/site/misterzeropage/

> I would not go that far, but a VGA card, VGA CRT, a serial mouse and an XTIDE card with a CF card in it, and it would be a lot easier to use…

The downside, my Cherry MX blue switches feel like second class now.

## UPDATE

When I was installing my VM with `PC DOS`, at the end of the installation I was aske if I wanted to start in `shell` mode. It turns out there is a command `DOSSHELL` (needs to be executed fron `C:\DOS`) which gives you a very fancy
gui.

{{< image "images/dosshell.jpg" Fit "600x600" >}}
😱 It has a GUI.
{{< /image >}}

## UPDATE 2

I recently received some awesome feedback from [Liam Proven](https://disqus.com/by/liamproven/). If you read through the post there will
be updates with the feedback. Thanks for the feedback @Liam.


