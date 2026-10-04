---
layout: post
title: Virtualized 5G Network Slicing
feature-img: "assets/dashboard-5g.png"
img: "assets/dashboard-5g.png"
date: 15 April 2026
tags: [5G, Networking, Capstone]
---

### Capstone Project · Carleton University · Oct 2025 – Apr 2026 · 🏆 Best Video Award, Capstone Showcase

- Built a 5G standalone core (free5GC v4.1.0 + UERANSIM v3.2.6) across KVM virtual machines
- Two slices simulating a hospital network: an isolated URLLC slice for ICU patient vitals, a shared eMBB slice for telemedicine/radiology data
- Flask dashboard with SSH remote control of every VM and live tunnel/patient-data monitoring over MQTT
- Simulated a DDoS attack from a third UE through the 5G tunnel — the shared slice congested while the isolated URLLC slice stayed fully operational
- UDP load testing with iperf3 (bitrate, jitter, packet loss) from 10 to 110 parallel streams
- [View project](https://github.com/sidhantkumar0/CAPSTONE-5G-SLICES)
