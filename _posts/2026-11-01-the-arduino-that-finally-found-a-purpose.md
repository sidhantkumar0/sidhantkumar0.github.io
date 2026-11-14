---
layout: post
title: "The Arduino That Finally Found a Purpose"
date: 2026-11-01
tags: [Arduino, Monitoring, Homelab]
feature-img: "assets/arduino-on-cisco-3850.jpg"
---

I had to buy an Arduino starter kit for my Real Time Systems class. I used it for the class, and when the class was done, the kit went into a drawer and stayed there.

Then I started building a home lab. The cabinet started filling up with the kind of gear that runs warm: a PC I turned into a server, a Cisco 3850, and four Raspberry Pis. I kept wondering if it was getting too hot in there, and I had no way to know. The switch and the server have their own fans and their own warnings, but the cabinet itself had no thermometer at all.

That is when I remembered the drawer. I dug out the old starter kit box, and in the parts list there was a DHT11 sensor that reads temperature and humidity. That was the answer, and it was already mine.

The setup is simple. The DHT11 sits in a small case I 3D printed, stuck to the inside wall of the cabinet. Three wires run down to an Arduino Uno in a blue case I printed, sitting on top of the Cisco switch. The Arduino plugs into one of my Raspberry Pis over USB.

![The DHT11 sensor in its 3D printed case, wired down to the Arduino Uno in its blue case](assets/arduino-sensor-closeup.png)

A small Python script reads three numbers off the serial port: temperature, humidity, and heat index. It exposes them as Prometheus metrics, and the script runs as a pod in my K3s cluster, pinned to the Pi the Arduino is plugged into, because the pod has to run where the USB device is. Prometheus scrapes it every 15 seconds. Grafana draws the graphs, and Alertmanager emails me if the temperature goes over 30 degrees or if the sensor goes quiet for 10 minutes.

![A week of temperature, humidity, and heat index readings on the Grafana dashboard](assets/grafana-homelab-thermo-7days.jpg)

The dashboard now holds a week of readings. Temperature sits around 25 to 27 degrees, and the heat index tracks close behind it. It is not a hot cabinet, which is good news, but now I would know if that changed.

![The arduino exporter and the monitoring stack running as services in the cluster](assets/headlamp-cluster-services.jpg)

Two things went wrong along the way, and both were worth learning from. The first was the dashboard itself. One morning it showed no data at all, even though the sensor was fine and Prometheus had the readings. The problem was the dashboard time range, which had been left on a fixed window in the past. The data was there, the graph was just looking at the wrong hours. The second was simpler. I took the wires out and put them back, and the first thing I checked was whether the graphs came back live. They did, within a minute.

It is a small thing, and it is the part of the cluster I actually look at every day. A sensor you can see working beats a dashboard full of cluster metrics you never open. And it started as a class kit in a drawer, which is a good reminder that the parts you already own are sometimes the answer.

The sensor runs on the four Pi cluster I wrote about here: [From Dusty Drawer to Tiny Cloud](https://sidhantkumar0.github.io/2026-10-11/four-pi-kubernetes-cluster). The exporter code and the cluster setup are on GitHub: [Sidhants-Homelab](https://github.com/sidhantkumar0/Sidhants-Homelab).
