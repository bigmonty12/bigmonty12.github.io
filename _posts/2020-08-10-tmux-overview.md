---
layout: single
title: "tmux: not for schmucks"
categories: tmux
permalink: /tmux-overview
---
My life was flipped-turned upside-down in the year 2019. 
![FreshPrince](https://1.bp.blogspot.com/-f0Larc0ouIQ/UTEH51UtGzI/AAAAAAAAI7E/DeeeZqHzye4/s1600/freshprinceofbelair.jpg)

For years (okay, mostly just a couple of summers), I had been using remote servers. I would ssh from my personal computer (or use PuTTY) to access our server. I often had long-running processes (I'm looking at you [Bowtie2](http://bowtie-bio.sourceforge.net/index.shtml)!) I needed to run. One of my biggest issues was that if my host computer lost connection to the server, my processes would also stop! This is a pretty big problem if you need to travel from one Internet connection to another (Or if your computer automatically restarts)! This led to me running my bioinformatics pipelines at night, when I knew I would have consistent Internet for a while. Of course, this was not ideal. Fast forward a couple years and ...

## tmux has entered the chat
![tmux](https://www.tecmint.com/wp-content/uploads/2016/01/Tmux-Manage-Multiple-Linux-Terminals.png)

Quite literally, the most important program in my workflow is [tmux](https://github.com/tmux/tmux/wiki). tmux is a terminal multiplexer, which essentially means it allows the user to have several programs running in one terminal, detach them so they can run in the background, and then reattach them in a new terminal! The setup is also incredibly customizable. 

Okay, sounds pretty cool, but your most important? Seriously? Seriously. Let's say my supervisor emails me at the end of the work day and tells me there are some freshly sequenced ATAC-seq samples. I want to start my [ATAC-seq pipeline](https://github.com/bigmonty12/BASS), but I know it will not finish by the time I leave work for the gym. I can spin up a new tmux session, start my pipeline, detach the session and go do some heavy squats without even worrying about my connection malfunctioning. After I get home and eat some dinner, I want to see if my processes have finished. I simply ssh back into my server and attach my tmux session. It is like I never even left for the gym (just as my chicken legs would seem to imply)!

![Squat meme](https://www.memesmonkey.com/images/memesmonkey/fe/fe48cfcbeed7939b45fef9822a145a12.jpeg)

I find tmux useful when working on different projects, as well. Right now, I have three different tmux sessions saved, each for a different work project. It is quite handy to just reattach a session and pick up right where you left off, especially if it has been a few days since working on that specific project. The session can even be named and renamed, making it easy to keep track of your work. 

Now, I am not going to get into the tmux key bindings or configuration. Nor will i pitt tmux and [screen](https://linux.die.net/man/1/screen) against each other. That's not the purpose of this post. I am much more interested in just bringing this to the attention of beginner (and maybe non-beginner) bioinformaticians! tmux (or maybe screen) is an essential program for maximizing your efficiency. Use it! I promise you will thank me later!

### Links about tmux

[How-to Geek's how to on tmux](https://www.howtogeek.com/671422/how-to-use-tmux-on-linux-and-why-its-better-than-screen/)
[Ham Vocke's guide to customizing tmux](https://www.hamvocke.com/blog/a-guide-to-customizing-your-tmux-conf/)
[Barbarian meets coding](https://www.barbarianmeetscoding.com/blog/2019/12/25/jaimes-guide-to-tmux-the-most-awesome-tool-you-didnt-know-you-needed)

### Fin

For those of y'all who already use tmux, what keeps you using it? What other resources have y'all used to increase your tmux skills?



