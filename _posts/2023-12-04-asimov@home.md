---
layout: post
title:  "asimov@home"
date:   2023-12-04 10:15:00 -0500
categories:
---

# asimov@home is online

Over the last few days I have been knee deep in Docker compose and exploring the great services available at [awesome-selfhosted](https://awesome-selfhosted.net/). I don't have money to put towards reserving cloud resources these days, so instead I've viewed it as a challenge to learn more about virtual networking and setting up a truly custom development environment.

Cloudflare tunnels (formerly Argo tunnels) have been amazing for this. The website you're currently browsing is hosted by GitHub pages for free, but it's limited to serving static HTML/CSS. I wanted to pack more features into my domain without sacrificing much security posture. What I *really* wanted to figure out was to see if I could serve consumable data analytics without opening up ports on my personal network. This would let me host web applications like Shiny dashboards without shelling out cash to keep them online. Cloudflare's tunneling agent, cloudflared, is perfect for that.

With a little elbow grease (and a lot of DNS troubleshooting), I put together a Docker compose file that stands up the entire asimov@home stack in seconds. It's pretty slick.

Right now there are some limitations - first of all, I'm still running the asimov@home stack on my personal Windows machine using WSL2. Of course, if I shut down my machine, the stack shuts down as well. More annoying is that the Docker daemon uses the WSL2 backend, which won't start unless I login. There are some hacky ways to get around this but what I'd rather do is just move asimov@home over to a dedicated NAS in the future instead of host it on my machine. But I'll have to table that for later (i.e. when I can afford to get more hardware).

What I *can* work on for now is improving the stack's architecture. I have a couple ideas here - for starters, I think I can move the frontend services (like the homepage) onto my RaspberryPi. That way if the main services go down, you'll still be able to see the asimov@home splash page. Along with this, I'll probably split out the main services out into their own compose files (and orchestrate them with K8s? Maybe??) so that way I can take down/stand up services individually as I edit their configurations.

But in the mean time, it's not too bad for now. You can visit [asimov@home](https://asimov.calcifer.cloud) today. You *probably* shouldn't get a 404. Probably. If you do, just know I'm likely somewhere deep inside Ubuntu tearing my hair out.

