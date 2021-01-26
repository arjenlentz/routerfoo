Arjen's abstract for Linux.conf.au 2021's SysAdmin miniconf, Sat 23 Jan 2021
arjen (at) lentz (dot) com (dot) au

Building my own border router
-----------------------------
I'm not a sysadmin, but sometimes I have to do stuff - and I have to do security, for a living but also to keep the home network safe and performant.
Consumer routers suck: in performance, connection reliability, security, and ability to have a sane configuration.
OpenWRT and DD-WRT are nice, but sometimes one has this weird urge to just do it again, from scratch and using open bits whereever possible.
Maybe just because.

Anyway, I decided to order two PC Engines APU 4d4 boards from the awesome Pascal Dornier in Switzerland <https://pcengines.ch/>. These are cheap-ish (EUR 99) little fan-less single board computers with a 1 GHz AMD GX-412TC 4 core CPU (64-bit, of course), 4GB RAM, 4x Gbit Ethernet ports, and plenty of other connectors and options. I put in a PCIe SSD card.
I first talked to the board's BIOS via a serial cable (was already up-to-date, good), and installed Debian 10 on it (with some minor hackery) from a USB stick.

And behold, my NBN HFC connection is now stable, and faster.

Maybe you would like to do something similar, or maybe you just want to pick up a few of the things that I've done - you can do any of this with a regular Linux box as well:
* A few of the ports are configured as a switch, using bridged network interfaces.
* One port talks to the NBN HFC modem with PPPoE connection and a VLAN, insisting it's actually the original ISP-provided device.
* IPv4/IPv6 native dual stack, each with subnets (I just have those, from when I ran a company from home)
* ~~Outbound rate-limiting on the HFC connection to keep NBN happy~~ *(turns out not to be needed with this router/config! It wasn't NBN but the ISP's router)*
* Appropriate kernel tuning via sysctl - seemingly quite necessary for dealing with funny traffic!
* A hand-crafted effective firewall, providing safety but also (when desired) insights in what fun tries to scan and gain access, how and from where.
* Configuring ~~Unbound DNS~~ DNSmasq to get rid of most ads on the LAN. *(Unbound is great, if you don't want the dns-ip-gate trickery, you can use it instead)*
* Surviving a reasonably-sized DDoS or other attack without flinching too much.
* Using dynamic geo-blocking, again with options to gain insight.
* WireGuard VPN end-point, both for my own devices and for geo-tunneling (using policy routing) *(* see below for a WireGuard love story)*
* Optional RKhunter and Suricata intrusion detection/prevention.
* Being invisible for scans, if so desired.
Extra options are adding mobile data backup with an on-board SIM card (may do), and wifi.

In this talk I will show what it all looks like on the outside and inside, and go over the configuration - understandable for small league nerds.
So you can do this yourself, or just learn more about how the various bits work.
(Some entertaining stuff-ups and anecdotes are also included.)

A WireGuard love story
----------------------
What if there was a VPN that only requires a few thousand lines of code, and lives inside the kernel?
Horays! Thanks to Jason Donenfeld, WireGuard is now available in recent Linux kernels, and otherwise easy to add.
But how to set it all up? The documentation is kinda all there, but mostly if you already know your stuff.
Tutorials abound, but some things have changed since. Aargh.

So now that the dust has settled, let's look at this from the non-whizz perspective.
How to peer, or set up a server with clients, or a network tunnel with policy routing.
I'm not the expert, but I've made it work and I can explain what I did.
