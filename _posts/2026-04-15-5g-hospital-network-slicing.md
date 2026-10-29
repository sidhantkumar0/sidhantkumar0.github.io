---
layout: post
title: "I Attacked My Own 5G Hospital Network to Prove the ICU Slice Would Survive"
date: 2026-04-15
tags: [5G, Networking, Capstone]
feature-img: "assets/dashboard-5g.png"
---

Here's a sentence I never thought I'd write: I spent my final year at Carleton attacking a hospital network.

Relax, it was our own virtual one. It was my capstone project at Carleton (Oct 2025 to Apr 2026), and the whole point was to find out whether 5G network slicing could actually protect the traffic that matters most when everything else on the network is falling apart.

My part? The 5G Core, the Dashboard, and the Attack Setup.

We built the whole thing with open source tools, free5GC version 4.1.0 for the core and UERANSIM version 3.2.6 for the simulated phones and radios, all running on virtual machines through KVM. No carrier gear, no telecom lab budget, just a full 5G network running on computers we already had. That was the beauty of it. Anyone with a decent machine could build this.

The Hospital, Sliced Up

Picture a hospital running on this network, split into slices. A slice is just a private lane on the same network, with its own rules about who gets in and how much room they get.

Our hospital had two.

The first was an isolated slice for ICU patient vitals, the kind of traffic that cannot wait. It got its own lane, cut off from everything else. In 5G speak that is called a URLLC slice, which is a fancy way of saying ultra reliable and instant.

The second was a shared slice for the everyday hospital stuff, video calls for telemedicine and scans moving between departments. That one is called an eMBB slice, basically the fast lane for big data.

```
┌─────────────────────────┐  ┌─────────────────────────┐
│ ICU patient vitals      │  │ Video calls and scans   │
│ URLLC slice, isolated   │  │ eMBB slice, shared      │
└─────────────────────────┘  └─────────────────────────┘
```

The Attack

Then came my favourite part. We added a third phone to the network, and its only job was to be a menace. It flooded the shared slice with a DDoS attack through the 5G tunnel, the same way a real attack would try to choke a network.

On top of that, we hammered the network with load tests, pushing UDP traffic from 10 parallel streams all the way to 110, and watched three things the whole time: bitrate, jitter, and packet loss.

The Result

The shared slice did exactly what you would expect. It congested, slowed down, and struggled under the flood.

The ICU slice didn't even blink. Vitals kept flowing, instant, the whole time, while the attack raged on the lane next door. That was the moment the project clicked for me. Slicing isn't just a nice idea on a slide. When it's set up right, the isolation is real, and it holds when it matters.

The Dashboard

None of that would have been visible without the dashboard. I built it with Flask, and it gave us remote control of every virtual machine over SSH, plus live monitoring over MQTT. Patient data moving, tunnels up, attack traffic climbing, all of it on one screen while the test ran. Watching the ICU numbers stay flat while the shared slice melted down is still one of my favourite sights from the whole degree.

Final Thoughts

The project won the Best Video Award at the Capstone Showcase, which was a great way to finish it, and my supervisor Prof. Ashraf Matrawy deserves a lot of credit for steering us through it.

If there is one thing I took away from it, it's this: I learned more about how 5G actually works by building a core, breaking a network, and fixing it again than I ever could have from reading about it. Theory tells you slicing should work. Watching an ICU slice survive a flood tells you it does.

The code lives here: https://github.com/sidhantkumar0/CAPSTONE-5G-SLICES
