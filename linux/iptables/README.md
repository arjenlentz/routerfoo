# IP tables
So iptables is extensive. Yeah. Google, Cloudflare, etc run on Linux, too. It can do the job!
Peruse "man iptables-extensions" for fun and education.
Also refer to the Netfilter diagram (ref below, at Wikipedia and kept up-to-date) as it shows what happens where.

## But NetFilter?
Yes. iptables already isn't what the kernel does, Netfilter currently just provides the legacy iptables interface.
In about three or so major kernels versions, the old iptables interfaces are going to go away completely.

However... while most of what we do can be done in Netfilter magic, ipset is not quite the same.
I'm pretty sure the equivalent can be done, but I haven't worked that out yet.
Insights welcome!

## General guides we run by
Cloudflare says: “If you’re going to drop a packet, do it as early as possible.”
1. Raw
2. Mangle
3. Filter
4. NAT

Arjen says: “The less noise I let in, the less noise I have to monitor.”
1. LOG what we want to be filtering. Patience! Am I happy with what it catches? (anything?)
2. DROP those weird packets
3. Regularly grep around in /var/log/syslog to see what we’ve caught
4. Use Cloudflare’s mmwatch 'sudo iptables-save -c | egrep "^\["' | grep -v "LOGDROP "

Ref.
- <https://en.wikipedia.org/wiki/Netfilter#/media/File:Netfilter-packet-flow.svg>
- <https://github.com/cloudflare/cloudflare-blog/tree/master/2017-06-29-ssdp>
