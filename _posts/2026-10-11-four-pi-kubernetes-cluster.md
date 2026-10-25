---
layout: post
title: "From Dusty Drawer to Tiny Cloud: Building a Kubernetes Cluster with Four Raspberry Pis"
date: 2026-10-11
tags: [Kubernetes, Raspberry Pi, Homelab]
feature-img: "assets/WhatsApp Image 2026-10-02 at 1.15.17 PM (2).jpeg"
---

I had two Raspberry Pis lying around in a drawer, constantly staring at me with unused potential. They’re lightweight, energy-efficient, and far too capable to just sit there gathering dust. Driven by the itch to build something cool, I decided to build a homelab cluster—and quickly picked up two more Pis off Facebook Marketplace to round the squad out to four.

My main goal? Learn DevOps hands-on.

After diving down a research rabbit hole, I chose K3s over full-blown Kubernetes. K3s is a lightweight, production-ready distribution designed specifically to thrive on resource-constrained hardware like the Pi. The best part? It uses standard kubectl commands, so every concept and trick I learn here transfers directly to enterprise-grade Kubernetes environments.

The Setup & Architecture

Here is how the four-node setup breaks down:

pi-server3: The control plane (master node managing the orchestration).

pi-server1, pi-server2, pi-server4: The worker nodes handling the workloads.

```
       [ Cisco 3850 Switch (Trunked VLAN 20) ]
                          │
       ┌──────────────────┼──────────────────┐
       │                  │                  │
┌──────────────┐   ┌──────────────┐   ┌──────────────┐   ┌──────────────┐
│  pi-server3  │   │  pi-server1  │   │  pi-server2  │   │  pi-server4  │
│ (Control)    │   │   (Worker)   │   │   (Worker)   │   │   (Worker)   │
└──────────────┘   └──────────────┘   └──────────────┘   └──────────────┘
```

![The four Pi cluster](/assets/WhatsApp%20Image%202026-10-02%20at%201.15.17%20PM%20%282%29.jpeg)

Network isolation was a big priority for me. The entire cluster lives on its own dedicated network (VLAN 20, isolated on the 192.168.20.x subnet) trunked off my Cisco 3850 switch. This keeps my experimental lab traffic completely segregated from the rest of my home network.

Early Pitfalls & Lessons Learned

Setting up a homelab is rarely smooth sailing, and I hit a couple of classic roadblocks that ate up a few evenings:

Multi-Interface Traps: Every Raspberry Pi has both onboard Wi-Fi and an Ethernet interface. K3s automatically binds to an available interface on startup, and it lovingly chose my standard Wi-Fi network instead of my dedicated VLAN. I had to explicitly pin the node IPs to their respective 192.168.20.x addresses to ensure inter-cluster traffic stayed on the wired subnet.

Kubeconfig Permission Snags: Accessing the cluster via local commands threw permission errors early on. I resolved this by properly copying the generated K3s configuration file over to root's ~/.kube/ directory with correct permissions.

Small details, but they are exactly the kind of configuration quirks that consume hours if you aren't prepared for them!

What’s Running in the Cluster?

Once the foundation was stable, I started deploying actual services:

Headlamp: I picked Headlamp over the standard Kubernetes Dashboard because of its clean UI and ability to display CPU and memory utilization per node at a single glance.

Prometheus Stack: Full-fledged monitoring and metric collection across the entire cluster.

IoT Sensor Workload: I migrated an old Arduino temperature and humidity sensor—which previously ran as a basic Python script on a single Pi—into a containerized pod inside the cluster. It now streams live environmental metrics directly into Prometheus.

![Arduino temperature and humidity sensor](/assets/WhatsApp%20Image%202026-10-02%20at%201.15.17%20PM%20%281%29.jpeg)

3 Honest Gotchas Before You Build Your Own

If you're thinking about tackling a similar project, keep these three constraints in mind:

⚠️ Architecture Compatibility (arm64 vs amd64): Not every Docker image on Docker Hub supports ARM architecture. Always check for multi-arch or arm64 support before pulling an image, or you'll be debugging immediate crash loops.

⚠️ RAM Limits: Pis are memory-constrained. You need to strictly set resource requests and limits on your pods to avoid running out of memory (OOM).

⚠️ MicroSD I/O Bottlenecks: MicroSD cards are convenient, but they are slow and wear out under heavy write operations. Don't expect SSD-level performance out of standard cards.

What’s Next for the Lab?

This project is far from finished. My immediate roadmap includes:

Disabling Wi-Fi entirely across all nodes to force 100% Ethernet reliability.

Adding Pi-hole as a clustered DNS service down the line.

Final Thoughts

If you have a spare Raspberry Pi or two gathering dust, build a cluster. The entire project cost me very little beyond the two secondhand boards, and I have learned more from diagnosing and configuring this physical cluster than I ever could have from purely reading Kubernetes documentation.

Have you built a homelab cluster or experimented with K3s? Let me know what services you're running in the comments below!
