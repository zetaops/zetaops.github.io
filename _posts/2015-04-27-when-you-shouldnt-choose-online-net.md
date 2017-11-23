---
title: When you shouldn't choose online.net?
author: Gokhan Boranalp
---

Hiya devs and ops,

In this blog post i'll try to explain in which circumstances you shouldn't choose online.net dedicated servers for your projects.

Your keywords are, Openstack, CEPH, CoreOS, etcd, Neutron, latency, private network, distributed computing. If you have these keywords in your project, basically check for alternates of online.net
If you are wondering the root cause of all this mess please read on.

tl;dr be warned!

As an innovative software development company, we have several research projects. We wanted to have bare metal power of dedicated servers instead of public clouds. So we have innocently searched and found online.net. It seemed reasonable with Dell servers. What a big mistake!

Since the nature of our projects embraces a lot of different techniques, we have decided to setup Openstack at first. Because Openstack would let us install and play with several different components at the same time.
We have planned one controller node, three compute nodes and one management node with all the needed Openstack elements. As you can see, no redundancy on controller.

Nova for compute nodes
Cinder for volumes
Glance for images
CEPH for block storage
Neutron for networking
Horizon for UI
Keystone for identity
Of course all inter communication of the elements should be on private network without exposing to outside world.

We have just bought 5 servers at the beginning. And started to install one by one. Later on, we have found that we should deal with more complicated parts of the online.net. The great wall of the online.net private network namely RPN.

It says we can have Real Private Network (RPN) bandwith 100 Mbit/s - 1 Gbit/s on their site. Guess what, RPN network was limited to 100Mbit/s unless otherwise you upgrade to Business service level. Good work Monthy.
So we have upgraded service levels on every server to have 1 Gbit/s traffic.

Later on we have found that failover ips are not a good way to work with Openstack. Because failover ips are single ips and it is impossible to attach them for virtual machines as i.e. /24 notation block to Neutron.

We had to buy Ripe block to assign public ips to virtual machines. You can imagine the time we have lost till we come up with this solution.

After endless nights, finally we had a system working with all the components. BUT! While we are doing regular tests we have found another crucial problem. CEPH based mounted volumes I/O could only goes up to 8 Mbit/s. It was unacceptable of course. We have checked hell a lot of possible points to properly solve the problem.
We have done tests with iperf. We have seen no problem on speed. But still CEPH nodes had a latency problem. Because CEPH was using chatty protocol to communicate it's each nodes and adversely iperf has a single shot.

While we were fighting with the slowness problem, our controller node suddenly disappeared :(
On control panel only a short notification attached "Your server seems participated to a DDOS attack."

There was only one option on the panel. REINSTALL everything from the zero point. We could access the server in rescue mode but it was impossible to return it back online. It seems our paranoid support staff don't believe that we can diagnose and remove even if we have a rootkits.

At this point, we have to gave up Openstack and planned to shift to CoreOS. This is another story why we have shifted from one to another.

We have installed CoreOS on 3 nodes. Started to test if etcd rund properly. Our test was easy. Bind etcd to private ip adresses. See if cluster members acknowledged each other. And then remove one node and check the rest of the cluster. When all members online there was no problem. BUT! When we have removed just one node all the cluster started to throw weird errors. Of course we have checked these errors and nothing actually came up to explain how running nodes can't find each other. etcd also uses a chatty protocol as CEPH.
We wanted to test and see if this is arising from our infrastructure or not. We have set 4 machine cluster at Digital Ocean. Exactly same config files and same private ips. We have removed the node and etcd had no problems. We have removed another and add the removed one back? No problem.
At this point we have returned back and asked help from online.net support. You can find all support messages below.

We have spent 5 months to experiment how one ISP infrastructure could screw your system. We have learned a lot of course. I will not mention the financial part of this adventure.
We have migrated all the system the Google Compute Engine for now.

I really don't want to waste my time anymore with them.
I have collected all the support tickets during our quest to setup our system. You can read the rest if you have steel nerves.

I wish this blog post could be useful anyone intends to setup a similar system.


{% include figure.html image="/images/2015-04-27/ticket1.png" %}

Humm their network infrastructure have some IDS, IPS and firewall with strict rules working on their RPN. The server suddenly locked up. It means any protocol including chatty protocols having fast communication will be marked as hostile.

{% include figure.html image="/images/2015-04-27/ticket2.png" %}

misc questions

{% include figure.html image="/images/2015-04-27/ticket3.png" %}
