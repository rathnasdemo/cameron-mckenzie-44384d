---
schemaId: urn:gala:schema:content-frontmatter:2.0.0
schemaVersion: 2.0.0
id: 01a1f05c-915e-729b-a98e-d09245da93c8
kind: article
title: Configure a Docker Nginx Reverse Proxy Image and Container
description: I show how to turn an nginx Docker container into a reverse proxy for a back-end application, then build images from it with docker commit and with a Dockerfile.
language: en-US
authors:
- 01a1f061-2b8f-7bbd-aa81-388605f00509
tags:
- docker
- nginx
- reverse-proxy
- dockerfile
- tomcat
status: published
createdAt: '2022-06-06T12:00:00.000Z'
publishedAt: '2022-06-06T12:00:00.000Z'
slug: configure-docker-nginx-reverse-proxy-image-container
hero:
  path: assets/content-configure-docker-nginx-reverse-proxy-image-container-hero.jpg
  alt: Thumbnail of the video "Configure a Docker Nginx Reverse Proxy Image and Container"
  role: informative
redirects: []
extensions: {}
---
*Adapted from the video [Configure a Docker Nginx Reverse Proxy Image and Container](https://www.youtube.com/watch?v=ZmH1L1QeNHk)*

> **TL;DR:** I show how to configure nginx as a reverse proxy inside a Docker container. I start an nginx container, copy out its default.conf file, add a location block with a proxy\_pass to my Tomcat application, copy the file back in, validate it and reload nginx. Then I create an image two ways: with docker commit from the running container, and with a Dockerfile that copies default.conf into the nginx image and is built with docker build.

I'm Cameron McKenzie, editor-in-chief at theserverside.com, and I want to quickly show you how to configure an nginx reverse proxy in Docker.

## Starting an nginx container

*[Watch from 0:09](https://www.youtube.com/watch?v=ZmH1L1QeNHk&t=9s)*

First we need a Docker container to run. I use a docker run command to name the container nginx-base, because it's the baseline for the reverse proxy we're about to create. I run it on port 80, as we usually do, using the latest nginx image from Docker Hub.

That starts nginx, and if I go to localhost in my browser I get a welcome message saying nginx is up and running.

## What I want the proxy to do

*[Watch from 0:48](https://www.youtube.com/watch?v=ZmH1L1QeNHk&t=48s)*

That isn't exactly what I want. It's great that nginx works as a file server, but I want it to work as a reverse proxy. I have an application running on port 8080 on a great big long IP address, and it uses the context root sample. I don't want users to have to type that in. I want them to go to nginx on localhost, ask for the sample application, and have that mapped to the application running on the back end, whether that's Apache Tomcat, Node, Angular or whatever. That is essentially configuring nginx as a reverse proxy, and right now it isn't doing that.

## Copying out the configuration file

*[Watch from 1:39](https://www.youtube.com/watch?v=ZmH1L1QeNHk&t=99s)*

Inside the nginx container there's a configuration file that, if tweaked properly, will turn nginx into a reverse proxy. I want that file, so I use a docker cp command to go into the nginx-base container, look in etc/nginx/conf.d, grab default.conf and copy it to my desktop. I check the spelling, because sometimes I make an error, press enter, and the file is copied.

I open it with **sudo nano default.conf** and there is the entire file.

## Adding the proxy_pass location

*[Watch from 2:52](https://www.youtube.com/watch?v=ZmH1L1QeNHk&t=172s)*

To configure this as a reverse proxy you add a new location setting. Anytime somebody asks for /sample, I want to route them to the Tomcat application running on port 8080. That means configuring a proxy_pass setting with the IP address, port number and application name (the context root) of the Tomcat server: 192.168.246.131:8080/sample. Make sure you have a semicolon at the end.

I press ctrl-o to write it out, maximize the screen to look over everything, check that the address matches, and press ctrl-x to exit.

## Copying the file back and reloading

*[Watch from 4:08](https://www.youtube.com/watch?v=ZmH1L1QeNHk&t=248s)*

The configuration is done, but it's in my local default.conf file, which is no good to me. I need to put it inside the Docker container, so I do the reverse copy: from the desktop file default.conf back into the nginx-base container at etc/nginx/conf.d. I double check the command, press enter, and it's pushed in.

We can validate the file with **sudo docker exec nginx-base nginx -t**, and the syntax is good. We can also use docker exec on nginx-base to ask nginx to reload the file, so it all runs without stopping and starting the container. The signal was processed.

## Seeing the reverse proxy work

*[Watch from 5:39](https://www.youtube.com/watch?v=ZmH1L1QeNHk&t=339s)*

If the file has been edited properly, we should no longer get a 404 when we refresh. And boom, nginx is now handling the /sample request. It forwards the request to the Tomcat application server, Tomcat processes it and sends it back to the nginx container, and the nginx container sends the response back to my browser. That is nginx working as a reverse proxy inside a Docker container.

## Creating an image with docker commit

*[Watch from 6:18](https://www.youtube.com/watch?v=ZmH1L1QeNHk&t=378s)*

What's next? We'd like to create an image based on that container, so we can start it anytime in the future rather than leaving just a container floating around.

I run **sudo docker images** first to see the images I have loaded: nginx, tomcat and sample. Then I use **sudo docker commit** to take the nginx-base container and turn it into a new image called nginx-proxy. Running docker images again shows nginx-proxy as a brand new image. I could even run it with **sudo docker run nginx-proxy**, and we have the proxy server running as our own image.

## Creating an image with a Dockerfile

*[Watch from 7:27](https://www.youtube.com/watch?v=ZmH1L1QeNHk&t=447s)*

Some people don't like that approach, so here's another way, using a Dockerfile. I create one with **touch Dockerfile** and open it with **sudo nano Dockerfile**. It sits on my local file system right next to default.conf.

In the file I start off with the latest nginx image, then copy the default.conf file that's in the same folder as the Dockerfile into etc/nginx/conf.d/default.conf. This is great if you keep editing default.conf and want to recreate the image, rather than starting an nginx container, copying a file out of it and updating it. You just run this command instead. I save with ctrl-o and exit with ctrl-x.

## Building the image

*[Watch from 8:56](https://www.youtube.com/watch?v=ZmH1L1QeNHk&t=536s)*

With the Dockerfile created, I run **sudo docker build** with the -t flag to tag the image as nginx-reverse-proxy, followed by a dot, which means look for the Dockerfile in the current directory. I transposed the tag flag and had to change it around, and as I said, it helps if you spell things correctly. This creates a brand new image, not from a snapshot of a container, but from the default.conf file and the Dockerfile.

Running docker images, we now have both the nginx-proxy image, created from a snapshot of the container, and the nginx-reverse-proxy image, created from the Dockerfile.

## Wrapping up

*[Watch from 10:18](https://www.youtube.com/watch?v=ZmH1L1QeNHk&t=618s)*

That is how you configure an nginx reverse proxy in a Docker container and create a couple of images you can use over and over again. If you enjoyed this tutorial, head over to theserverside.com, where we have lots of great tutorials on Docker, Kubernetes, Git, DevOps, microservices, Java, you name it. If you're interested in my personal antics, you can follow me on Twitter at cameronmcnz, and please subscribe on YouTube.

*[Watch the full video on YouTube](https://www.youtube.com/watch?v=ZmH1L1QeNHk)*
