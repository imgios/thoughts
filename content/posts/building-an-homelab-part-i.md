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
