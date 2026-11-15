---

layout: post
title: "From Hypervisor to Kubernetes: What Is Driving the Shift"
date: 2026-11-14
tags: [Kubernetes, Homelab, Proxmox]

---

Before COVID, virtual machines and hypervisors were the default. Now Kubernetes is taking over. I checked the numbers, and the real story is more interesting than that.

Kubernetes was already mainstream before COVID. In the CNCF survey from 2019, 78 percent of respondents were already running Kubernetes in production, up from 58 percent the year before. Containers were at 84 percent. So inside the cloud native world, Kubernetes had already won before the pandemic. What was true is that for the average company, virtual machines were still the default for most workloads. Kubernetes was for new apps, not for everything.

What changed is not Kubernetes suddenly appearing. What changed is VMware.

In November 2023, Broadcom bought VMware. A month later, perpetual licenses were gone. Everything moved to subscriptions, priced per processor core. The free version of ESXi went away in February 2024. People who renewed reported bills three to five times higher, and some reported ten times higher. AT&T sued over a price rise of about 1,050 percent.

That is the trigger. The shift since then is a VMware exodus, and the numbers are clear. A CloudBolt survey from February 2026 found 86 percent of VMware customers are actively shrinking their VMware footprint. Only 4 percent have fully moved off. Gartner expects 35 percent of VMware workloads to be on a different platform by 2028.

So are companies switching? Yes. Here are the ones I found through talking with people and researching online.

Computershare moved 24,000 virtual machines to Nutanix, after being quoted a price rise of ten to fifteen times. Beeks Group moved the majority of its virtual machines, more than 20,000 of them, to OpenNebula, an open source platform built on KVM, after its bill went up ten times. Emirates NBD, a bank in Dubai, moved more than 9,000 virtual machines to Red Hat OpenShift Virtualization. Cleveland Clinic is moving more than 10,000 virtual machines the same way, and expects its total cost to drop by half. Tesco is moving its store edge systems to Proxmox. AT&T sued Broadcom and settled, though it has not said where it is moving to. GEICO moved to OpenStack.

Notice the pattern. Most of these companies did not move from virtual machines to containers. They moved from VMware to another hypervisor. The Kubernetes part is subtler. Emirates NBD and Cleveland Clinic moved to OpenShift Virtualization, which runs virtual machines inside Kubernetes. That is the bridge: the virtual machines do not disappear, they just run on top of Kubernetes instead of on top of VMware.

Hardware adds to the pressure. A 32 GB DDR5 kit that sold for about 80 to 120 dollars late last year now sells for about 400 to 570 dollars, and TrendForce puts the rise at about 300 percent since September 2025. I could not find a source that proves hardware prices caused the Kubernetes shift, so I will not claim that. But the prices make density matter more, and that is where containers win. A virtual machine carries a full guest operating system, so every VM boots its own kernel and holds its own chunk of memory before your application even starts. A container shares the host kernel, so it uses only the memory its application uses, about two to four times less than a VM for the same workload. On a server with 128 GB of RAM, you can run about 100 to 200 containers, or about 10 to 15 virtual machines. When RAM costs 400 dollars for 32 GB, density is money.

K3s, the light build of Kubernetes, runs on a Raspberry Pi, which is why it shows up in so many home labs now. It is the same idea at a smaller scale: use less hardware better.

## The hypervisor is not dead

None of this means virtual machines are finished. They still win where isolation matters. A VM has its own kernel, so a crash or a breach in one machine does not touch the others. Linux Foundation Research found virtual machines still run 53 percent of production applications, and 71 percent of companies expect that share to stay about the same. Only 8 percent run their virtual machines on Kubernetes today. Gartner has warned there is no one for one replacement for VMware Cloud Foundation, and most companies that leave will shrink their VMware footprint rather than eliminate it.

## The takeaway

When hardware was cheap, the easy answer was a bigger box and more virtual machines. That answer does not work anymore, not at these prices, and not with VMware priced the way it is now.

Kubernetes is not free. It has a learning curve, and the networking alone can take a full evening to get right. But once it runs, it lets small hardware do real work, and that is what you need when every part costs two to five times what it did a year ago.

The hypervisor is not dead. It is just no longer the default. For the next service you add, ask whether it can run in a container first, and only give it a virtual machine if it truly needs one. That is the shift, and it started the day Broadcom changed what VMware costs.

I am writing this as someone starting out in networking and researching how to build things without spending a fortune, not as someone who has it all figured out.

Sources:

- CNCF Annual Cloud Native Survey 2025: https://www.cncf.io/announcements/2026/01/20/kubernetes-established-as-the-de-facto-operating-system-for-ai-as-production-use-hits-82-in-2025-cncf-annual-cloud-native-survey/
- CNCF 2019 Survey results: https://www.cncf.io/blog/2020/03/04/2019-cncf-survey-results-are-here-deployments-are-growing-in-size-and-speed-as-cloud-native-adoption-becomes-mainstream/
- Channel Dive, CloudBolt VMware survey: https://www.channeldive.com/news/broadcom-vmware-migrations-costs-cloudbolt-report/812735/
- The Register, Gartner on leaving VMware: https://www.theregister.com/virtualization/2026/05/12/quit-vmware-and-youll-emerge-with-more-complex-and-less-capable-infrastructure/5238442
- TechTarget, enterprises moving to OpenShift Virtualization: https://www.techtarget.com/news/Enterprises-fleeing-Broadcom-move-to-OpenShift-Virtualization/857133/