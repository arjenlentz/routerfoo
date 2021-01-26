# Disk Layout

Note: I used LVM + multiple partitions, but doh... you can do all this in BtrFS with [subvolumes](https://btrfs.wiki.kernel.org/index.php/Manpage/btrfs-subvolume)!
If you do go down the BtrFS path, also create a @root subvolume and mount it as your root device instead.

**Security**: mounts are either writeable by non-priv users, or executable, but never both.
An elaboration on the [Debian Security Manual](https://www.debian.org/doc/manuals/securing-debian-manual/ch04s10.en.html)

- /
  - /boot nodev
  - /usr nodev
  - /var nodev
  - /home nodev,nosuid,noexec
  - /tmp nodev,nosuid,noexec (see 00apt-routerfoo.example to make this work!)
  - Swap (file or partition)

I also tried the recommended "ro" on /usr but it tends to cause hassles when running programs still have files open there.
