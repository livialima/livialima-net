# How to Set Static IP Address on Linux

Different from desktop machines where you can use dynamic IP addresses, static IP address are often required on a server infrastructure.

## RHEL / CentOS / Fedora:

You will need to edit:

```
/etc/sysconfig/network-scripts/ifcfg-eth0
```

Where ```ifcfg-eth0``` relates to your network interface ```eth0```. If your interface name is ```enp1s0``` then the file that you will need to edit is ```ifcfg-enp1s0```.

Add the following fields:
```
DEVICE="eth0"
BOOTPROTO="static"
IPADDR="192.168.1.1"
NETMASK="255.255.255.0"
TYPE="Ethernet"
```

## Debian / Ubuntu:

To setup static IP address in Debian/ Ubuntu, edit the following file:

```
/etc/network/interfaces
```

You may see a line looking like this:
```
auto eth0
iface eth0 inet dhcp
```
Change it so it looks like this:
```
auto eth0
iface eth0 inet static
  address 192.168.1.1
  netmask 255.255.255.0
```

## Restart the networking on your system:

**SysVinit**: ```/etc/init.d/network restart```

**SystemD**: ```systemctl restart network```

If unsure of what which system manager your distro uses, try this:
```
pidof systemd && echo "systemd" || echo "sysvinit"
```

## Conclusion

You now know how to configure a static IP address on a Linux distro.
