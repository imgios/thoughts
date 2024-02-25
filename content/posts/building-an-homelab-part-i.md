---
title: "Building an homelab — Part I"
date: 2024-02-24
draft: true
toc: true
tags: ["homelab", "docker", "kubernetes"]
keywords: ["homelab", "docker", "kubernetes", "k3s", "raspberry pi"]
summary: "Building an homelab with spare hardware and Raspberry Pis can be funny as well as educational. This post covers a Kubernetes homelab built by using two Raspberry Pi 4 nodes."
---

Spare hardware, Raspberry Pis, servers and mini PCs. What are they? Is it a shopping list? Well, no. These are things that IT enthusiasts usually use to set up a homelab.

Homelabs are made to address different needs and/or purposes. They can be a place to learn and experiment new topics or a safe environment to spin up self-hosted services. Some common use cases are:
- Build an own private cloud to store your files
- Build your own streaming platform (for educational purposes 👀)
- Build an ephemeral playground for a specific topic

Building an homelab can be easy as spinning up some Docker containers on a given machine or complex as setting up a Kubernetes cluster with several nodes. Furthermore, they can be cheap by using spare hardware or expensive buying new hardware to use.

You decide.

## Why am I building an homelab?

In my case, I'm building it to explore a bit more several topics, such as:
- System administration
- Self-hosting some services
- A bit of home automation
- Experiment new topics

I would like to get better in system administration and in container devlopment and orchestration. Furthermore, I would also like to get a small Kubernetes cluster running at home with low power usage that I can use to host some services, such as Home Assistant, Prometheus, Grafana, and so on.

Is it overkill? Maybe.

I imagine it as a huge and long truck used to deliver a small package, but an homelab also gives me the right amount of fun while getting my hands dirty with cables, boards, configurations and so on!

## Homelab topology

As I said before, reusing spare hardware can be a good option to start with an homelab. Actually, my homelab will be composed by:
- 2x Raspberry Pi 4 8GB
- TP-Link Switch

Currently, the only "spare" hardware that will be used is the switch, meanwhile the Raspberry Pis are brand new. I decided to start this homelab easy with just few nodes, then I will see how it'll evolve.

![Homelab Topology](images/simple-homelab-topology.png)

## Preparation

There are few steps to do to configure the Raspberry Pis and set them a fixed IP, in this way they will always get the same IP even if they get rebooted for some reason. This can be done in three similar ways:
- The first method let us achieve that by updating the modem DHCP subnet mask that is usually set to **/24**, and this means that the modem can assing any IP in the range 192.168.1.1 - 192.168.1.254 (almost the entire subnet!). We can lower this subnet from /24 to /25, in this way the modem will be able to assign any IP in the range 192.168.1.1-192.168.1.127. This approach, leaves us a bunch of free IP from the range 192.168.1.129 - 192.168.1.254 (that's a lot!)
- Another way to achieve the same result is by updating the modem DHCP range instead of the subnet mask. Using this method, you can keep the default /24 as subnet mask, but you can define both DHCP range start and DHCP range end by setting them to 192.168.1.2-192.168.1.210, in this way you will be able to use any IP from 192.168.1.211-192.168.1.254. Also in this case, you will have a lot of free IPs usable for your homelab.
- Then we have the easiest way to get a fixed IP for our servers: this method consists of updating the modem DHCP settings by letting it know that a machine with a given MAC address (e.g., 2a-a2-44-6b-0b-4a) will get a fixed (or static) IP (e.g., 192.168.1.211). In this way we still leave the entire subnet to the modem DHCP, but we make sure that a given number of IPs will be reserved for our servers.

At this stage, it doesn't matter which way will be used to get it working. I decided to use 192.168.1.211 for the first Pi and 192.168.1.212 for the second one.

Once the modem DHCP setting has been updated, I moved to flash the SD cards used to boot my Raspberry Pis. I had to struggle a bit on this step, not because it's hard but my Raspberry Pis decided to refuse the Raspberry Pi OS / Raspberry Pi OS Lite images. Said that, after several tries, I decided to go for the Ubuntu Server image. I used the Raspberry Pi Imager, selected the Ubuntu Server 64-bit image and customised the installation by providing the user to create with the password, the hostname, and the network IP to set to the board.

![Raspberry Pis Tower](images/raspberry-tower.jpg)

## Verification

Now that both SD card has been written, it's time to boot up the Raspberry Pis and verify if they are running the Ubuntu Server flawless with the IP I set during the image flash.

Let's connect to the first board using both user and IP set during the SD card flash:

```shell
PS C:\Users\imgios> ssh imgios@pi01
imgios@pi01's password:
imgios@pi01:~$ lsb_release -a
No LSB modules are available.
Distributor ID: Ubuntu
Description:    Ubuntu 23.10
Release:        23.10
Codename:       mantic
imgios@pi01:~$ ip a | grep 192.168
    inet 192.168.1.211/24 metric 600 brd 192.168.1.255 scope global dynamic wlan0
```

I'm able to access the board using both user and password set during the image flash. Furthermore, I saw that the board took the right IP and has the hostname `pi01` set before.

Let's check the same on the second board:

```shell
PS C:\Users\imgios> ssh imgios@pi02
imgios@pi02's password:
imgios@pi02:~$ lsb_release -a
No LSB modules are available.
Distributor ID: Ubuntu
Description:    Ubuntu 23.10
Release:        23.10
Codename:       mantic
imgios@pi02:~$ ip a | grep 192.168
    inet 192.168.1.212/24 metric 600 brd 192.168.1.255 scope global dynamic wlan0
```
