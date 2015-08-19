<div class="separator" style="clear: both; text-align: center;">[![](http://3.bp.blogspot.com/-kulxUkG_EnM/VdQ5AuAw66I/AAAAAAAAANA/rEBWhAn0XB0/s200/docker.png)](http://3.bp.blogspot.com/-kulxUkG_EnM/VdQ5AuAw66I/AAAAAAAAANA/rEBWhAn0XB0/s1600/docker.png)</div>

As invaluable tools in networked and distributed systems research, network emulators and simulators offer a viable alternative to live experimental networks. In short, it's easier to draw a network using software and test it than to use real hardware. But before we start, let's go through one crucial point that will help us understand what we're trying to achieve.  

<div>  
**Simulators vs Emulators**</div>

<div>All tools that provide a testbed for networking scenarios fall into two categories: **emulators** and **simulators**.</div>

<div>Here's what Wikipedia says about the difference between those two:</div>

<div style="text-align: center;">

<div style="background-color: white; color: #252525; font-family: sans-serif; font-size: 14px; line-height: 22.3999996185303px; margin-bottom: 0.5em; margin-top: 0.5em; text-align: justify;">

> _Emulation differs from [simulation](https://en.wikipedia.org/wiki/Simulation "Simulation") in that a network emulator appears to be a network; end-systems such as [computers](https://en.wikipedia.org/wiki/Computer "Computer") can be attached to the emulator and will behave as if they are attached to a network. A network emulator emulates the network which connects end-systems, not the end-systems themselves.__Network simulators are typically programs which run on a single computer, take an abstract description of the network traffic (such as a flow arrival process) and yield performance statistics (such as buffer occupancy as a function of time)._

</div>

</div>

<div>Pure network **simulators** are mostly used in theoretical network research like new protocol algorithms. For example **ns-3** is an open source network simulator. That is, users can develop their own network protocol and simulate performance. It also has an animation tool to visually observe how their network operates and is used primarily in academic circles for research and education. **[GNS3](http://www.gns3.com/)**, one of the most popular network tools began as a Cisco emulation tool, but has grown into a multi-vendor network emulator. Every node in GNS3 is represents some network device, be it a **switch** in the form of a Cisco IOS image or a PC using some form of virtualization technology like **VirtualBox** or **VMware**. However, it's important to note that these nodes **emulate** real network devices.  As Wikipedia said, users can be attached to the emulator just like to a real network. So regardless of what GNS3 calls itself it's actually an **emulator** and a very useful tool for network administrators that design **real** networks with **existing** protocols, not experiments with network protocols that help write research papers.  

<div class="separator" style="clear: both; text-align: center;">[![](http://2.bp.blogspot.com/-1dYLghmkAgw/VdRZfwdeNHI/AAAAAAAAANU/Aikxpa9fdig/s400/netsim_trends.png)](http://2.bp.blogspot.com/-1dYLghmkAgw/VdRZfwdeNHI/AAAAAAAAANU/Aikxpa9fdig/s1600/netsim_trends.png)</div>

Some network tools call themselves emulators but are simulators but most tools that call themselves simulators are actually emulators. Another example is **[IMUNES](http://imunes.net/) **_(Integrated Multiprotocol Network Emulator/Simulator)_ which can't decide if it's an emulator or a simulator. It's an emulator. One good reason for calling an emulator a simulator is that users generally tend to google "network simulator" more often than "network emulator" so it's harder to get googled if you're called an emulator.  

The best network emulators generally have graphical interfaces that let users drag and drop network components into a sandbox to set up a network environment and then run experiments on those environments. Usually, those components (**network nodes** in the sandbox) represent your off-the-shelf network equipment: switches, routers, PCs etc. Different emulators use different techniques to implement those components. GNS3 uses a combination of Cisco IOS images for switches an routers and various virtualization technologies (VMware, VirtualBox, Docker, VPCS) to implement PCs. IMUNES uses Jails on FreeBSD and Docker on Linux to emulate all of its nodes. Basically, every node in IMUNES is either a FreeBSD or a Linux virtual machine, depending on which OS you're running it. So a router in IMUNES is actually a VM with a mainstream OS and special setup (e.g. some kind of routing software).  

Both IMUNES and GNS3 virtual machines can be anything the OS they run supports. If someone asks what is a good general-purpose OS to use for networking the answer will in most cases be **Linux**. Indeed, Linux is a good choice for a generic network node used in emulators. Let's simplify things and temporarily assume we want to build a network emulator that only uses virtualized Linux machines as nodes because we can set up a variety of network services on those machines like **Apache, Nginx, dhcpd and Nginx**. We couldn't do that if we only used components like Cisco routers. Sure, we could test a proprietary network protocol but we couldn't really stress test our new Gunicorn+Nginx setup. So generic nodes do have their uses in the world of network emulators. In the next part we'll talk about how to efficiently create such generic network nodes using some popular virtualization technologies.  

</div>
