# Software (Linux)

- Install from USB + serial console
- Debian 10
  - could be Ubuntu 20.04, but you'll need to tweak the image to enable serial, which Debian has by default
- LUKS, if you want
- LVM + ext4, or BtrFS (if you use BtrFS you won't need LVM)
- USBguard
- Optionally RKhunter, Suricata
- bridge-utils, vlan, pppd, hostapd (for wifi)
- iptables/ipset, iptables-persistent, DNSmasq
- OpenSSH, Mosh, screen, vim
- WireGuard - needs backports repo in Deb10
