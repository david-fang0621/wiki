My solution was to delete and re-add the network interface:

1. Shutdown your VM
2. Go to "Edit Virtual Machine Settings" and remove your network adapter
3. Boot your VM and turn it off
4. Open the .vmx file with your editor and delete all lines which start with "ethernet0”
5. Boot your VM and turn it off
6. Go to "Edit Virtual Machine Settings" and add a new network adapter
7. Boot your VM and open a terminal
8. Execute ip link. The output shows all the interfaces like this:

```bash
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: ens33: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN mode DEFAULT group default qlen 1000
    link/ether 00:0c:29:a5:cd:b6 brd ff:ff:ff:ff:ff:ff
```

1. Find your interface (ens33 in my case) and set it to up:

```bash
sudo ip link set ens33 up
```

1. Let your interface search an IP Address:

```bash
sudo dhclient ens33 -v
```

1. Worked with Windows 10 Host, Ubuntu 19.10 Guest and VMware Workstation 15 Player.
