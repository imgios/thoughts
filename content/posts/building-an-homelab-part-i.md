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
- Experiment new topic (e.g., GitOps)
