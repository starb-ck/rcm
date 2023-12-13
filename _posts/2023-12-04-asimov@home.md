---
layout: post
title:  "asimov@home"
date:   2023-12-04 10:15:00 -0500
categories:
---

# asimov@home is online

Over the last few days I have been knee deep in Docker compose and exploring the great services available at [awesome-selfhosted](https://awesome-selfhosted.net/). I've viewed this as a challenge to learn more about virtual networking and setting up a truly custom homelab container architecture.

The website you're currently browsing is hosted by GitHub pages for free, but it's limited to serving static HTML/CSS. I wanted to pack more features into my domain. What I *really* wanted to figure out was if I could serve consumable data analytics without opening up ports on my personal network. This would let me host web applications like Shiny dashboards without sacrificing much security posture. Cloudflare's tunneling agent, cloudflared, is perfect for that.

With a little elbow grease (and a lot of DNS troubleshooting), I put together a Docker compose file that stands up the required container stack in seconds. It's pretty slick.

![Home-lab architecture diagram](assets/posts/vhome-lab.gif){:width="100%"}

There are some limitations - first of all, I'm still running the asimov@home stack on my personal machine. Of course, if I shut down my machine, the stack shuts down as well. What I'd rather do is move asimov@home over to a dedicated NAS in the future instead of host it on my machine. But I'll have to table that for later when I can pick up some more hardware.

What I *can* work on for now is improving the orchestration. I have a couple ideas here - for starters, I think I can move the frontend services (like the homepage) onto a RaspberryPi. That way if the main services go down, you'll still be able to see the asimov@home splash page. Along with this, I'll probably split out the main services out into their own compose files (and orchestrate them with K8s? Maybe??) so that way I can take down/stand up containers individually as I edit their configurations.

It's not too bad for now. What this all means is that I can now self-host web-apps like this [CDC WONDER dashboard](https://shiny.calcifer.cloud/demos/cdc-wonder-cod). I think that's pretty exciting, especially for maintaining a freelancing portfolio. 

Cheers,
-Carter