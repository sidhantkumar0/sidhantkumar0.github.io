---
layout: post
title: "NetBox Lasted a Day in My Homelab"
date: 2026-10-19
tags: [Homelab, NetBox, Kubernetes]
---

Here is a lesson I learned the expensive way. Not in money, in time: the best tool on paper is not always the best tool for your lab.

It started with a simple itch. I wanted one place for the whole homelab, every IP address, every subnet, every device, every cable, plus my own side notes. And, because I was feeling ambitious, I wanted my passwords in there too.

That last part was the first crack in the plan. NetBox is great at tracking inventory, but it's not a password manager, and anything I typed into a notes field would just sit in the database as plain text for anyone with access to read. So the plan changed before I even started. NetBox for the inventory, and a proper encrypted vault for the secrets. Luckily both were open source with Helm charts and ARM images, so both could live on the Pi cluster.

The Install

I installed NetBox on the control plane of the cluster in mid October 2026, through Helm. Chart version 8.3.92, its own namespace, a NodePort of 31082. The admin password lived in a file with tight permissions, never in git.

It was not a clean install, of course. The chart wanted the port written as text in quotes, not as a bare number, and a bare number fails its schema check. That one quirk cost me an evening of staring at an error message before I figured out what it wanted. Small thing, but it set the tone.

Too Much Tool

Once it was up, I lived with it for a day, and that was enough. It was slow and heavy for what I actually had: four Pis and a handful of devices. NetBox is built for teams running real data centres, with racks and racks of gear to track. My lab is a shelf.

So the next day I decided it had to go. A helm command to uninstall it and a kubectl command to delete the namespace, and it was gone. No drama, no sunk cost speech. If a tool doesn't fit, keeping it around out of guilt just costs you more evenings.

What Replaced It

For a while the plan was a Homer page or just a notebook. Then Trilium took the job. It holds my notes, my links, and my IP ranges, and it's light enough that I forget it's even there. It does a worse job than NetBox at being a network inventory, and a much better job at being the thing I actually open every day.

Final Thoughts

Try the big tools. That part I don't regret. You learn a lot from installing something properly, even if you end up deleting it. But match the tool to the size of the problem. A shelf of Pis doesn't need data centre software, and deleting a tool that doesn't fit isn't failure, it's the decision.

The lesson stuck with me: the right tool is the one you actually use.
