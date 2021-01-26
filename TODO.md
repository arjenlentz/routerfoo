# TODO - Please contribute!

## IPv6
This is I think the biggest one right now.
IPv6 support in all aspects of this repo: configs, scripts.
It's not a "problem" as such, it just needs doing.

Many things just need almost literal duplication from IPv4 to their IPv6 equivalents.
Note that IPv6 needs some more foo in the ICMP section of the firewall, as IPv6's functioning actually relies on it.

## ipset -> Netfilter
Convert the current ipset dependency to use Netfilter magic instead.
Unless I'm mistaken, all the other things can be done in Netfilter syntax as well.

### iptables -> Netfilter
Once the ipset functionality has been converted to use Netfilter, everything else can move too.

## Add your desires here
Don't go overboard, we're not trying to add the kitchen sink.
