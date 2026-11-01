# Installing Proxmox 
### Creating a USB Flashdrive Installer

Install the Proxmox VE image file using this [link](https://www.proxmox.com/en/products/proxmox-virtual-environment/overview) and use [rufus](https://rufus.ie/en/) and [balenaEtcher](https://etcher.balena.io/) to flash the image file into the USB flash drive for installation.

In my case, I used Rufus
![[Rufus.png]]

Enter the BIOS/UEFI on the computer while the USB Flash drive with the installer plugged in. Boot from the USB Flash drive and install Proxmox VE.

Install Proxmox via graphical interface to simplify the installation process.

If multiple physical drives is present in the system, ensure that the drive selected is correct. The installation would wipe data from the drive selected. RAID options can be selected if redundancy and file integrity is needed. This approach can be optimal for high availability system for scaling up in the future.

---
### Setting Up my Device

Currently there are no `sudo` package installed in Proxmox. In order to install sudo, logging in as `root` and installing `sudo` package is needed.

```bash
apt update && apt install sudo -y
```


Since I am using laptop as my Host PC, I disabled the hinge switch to access my device while laptop is close and to prohibit it to shutdown. It can be done using the following:
```bash
sudo nano /etc/systemd/logind.conf
```
Then edit the following lines to:
```
HandleLidSwitch=ignore
HandleLidSwitchDocked=ignore
LidSwitchIgnoreInhibited=yes
```
Save and exit.

Activate and apply changes using:
```bash
sudo systemctl restart systemd-logind.service
```

Closing the laptop lid would not make the system inaccessible and does not automatically sleep and shutdown.

To avoid using root as the main user for configuring the system, a secondary user with root or `sudo` privileges is created and added to the `sudo` group. Creating user and adding them to the `sudo` group using the following commands:
```bash
adduser yourusername
usermod -aG sudo yourusername
```
###### Setting up WiFi in Proxmox
Ideally, Wi-Fi on Proxmox is not suitable for a normal Proxmox bridge configuration but there are some workarounds. I currently (at the time) only have 1 ethernet cable and does not have a 5-port switch (I plan to purchase one). I decided to temporarily connect it to Wi-Fi.

The default network config found on `/etc/network/interfaces` is:
```
auto vmbr0
iface vmbr0 inet static
	address 192.168.1.16/24
	gateway 192.168.1.1
	bridge-ports nic0
	bridge-stp off
	bridge-fd 0
	
iface nic1 inet manual
```

First, find the Wi-Fi interfaces:
```bash
ip link
```
or
```
ip a
```

It should look like this:
```bash
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: nic0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel master vmbr0 state UP mode DEFAULT group default qlen 1000
    link/ether f4:39:09:77:6c:ea brd ff:ff:ff:ff:ff:ff
    altname enxf43909776cea
3: wlp3s0: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN mode DEFAULT group default qlen 1000
    link/ether dc:a2:66:2b:ca:7f brd ff:ff:ff:ff:ff:ff
    altname wlxdca2662bca7f
4: vmbr0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP mode DEFAULT group default qlen 1000
    link/ether f4:39:09:77:6c:ea brd ff:ff:ff:ff:ff:ff
```

The Wi-Fi interface is `wlp3s0`

Install the required packages first:
```bash
apt install wpasupplicant iw dnsmasq iptables -y
```
Then run:
```
iw dev
```
It should show:
```
root@node1:~# iw dev
phy#0
        Interface wlp3s0
                ifindex 3
                wdev 0x1
                addr dc:a2:66:2b:ca:7f
                type managed
                txpower 0.00 dBm
                multicast TXQ:
                        qsz-byt qsz-pkt flows   drops   marks   overlmt hashcol tx-bytes        tx-packets
                        0       0       0       0       0       0       0       0               0
root@node1:~#
```

###### Testing Wi-Fi connection
Before modifying Proxmox network bridge, testing if Wi-Fi interface can actually connect by creating a temporary configuration:

```bash
nano /etc/wpa_supplicant/wpa_supplicant-wlp3s0.conf
```

Paste this:
```
ctrl_interface=/run/wpa_supplicant
update_config=1
country=PH

network={
    ssid="YOUR_WIFI_NAME"
    psk="YOUR_WIFI_PASSWORD"
}
```
	Note to edit the SSID and PSK of the WiFi connection
Protect the file:
```bash
chmod 600 /etc/wpa_supplicant/wpa_supplicant-wlp3s0.conf
```
Then test:
```bash
wpa_supplicant -B -i wlp3s0 -c /etc/wpa_supplicant/wpa_supplicant-wlp3s0.conf
```
Then check:
```bash
iw dev wlp3s0 link
```
It should display:
```
Connected to 30:40:74:ae:24:3c (on wlp3s0)
        SSID: YOUR_WIFI_NAME
```
Check:
```bash
ip route
```
and:
```bash
ip addr show wlp3s0
```

If it works, change Wi-Fi config to permanent.

Create a backup of the current configuration:
```bash
cp /etc/network/interfaces /etc/network/interfaces.backup
```

Then edit:
```bash
nano /etc/network/interfaces
```
to:
```
auto lo
iface lo inet loopback

auto wlp3s0
iface wlp3s0 inet static
    address 192.168.1.16/24
    gateway 192.168.1.1
    wpa-conf /etc/wpa_supplicant/wpa_supplicant-wlp3s0.conf

auto vmbr0
iface vmbr0 inet static
    address 10.10.10.1/24
    bridge-ports none
    bridge-stp off
    bridge-fd 0

iface nic0 inet manual
```

###### Enabling IP Forwarding within Proxmox

The Proxmox host needs to act as a router between VMs `10.10.10.0/24` and local are a network `192.168.1.0/24`.

Edit:
```
nano /etc/sysctl.conf
```
Add:
```bash
net.ipv4.ip_forward=1
```
Then apply:
```bash
sysctl -p
```
Then verify:
```bash
sysctl net.ipv4.ip_forward
```
It should show:
```bash
net.ipv4.ip_forward = 1
```
Enable IP forward across reboots:
```bash
echo "net.ipv4.ip_forward=1" > /etc/sysctl.d/99-ipforward.conf
```
Apply the configuration:
```bash
sysctl --system
```

###### Configuring NAT

Anything coming from `10.10.10.0/24` network going out through Wi-Fi should be masqueraded as the Proxmox host.

```bash
iptables -t nat -A POSTROUTING -s 10.10.10.0/24 -o wlp3s0 -j MASQUERADE
```
Then allow forwarding:
```bash
iptables -A FORWARD -i vmbr0 -o wlp3s0 -s 10.10.10.0/24 -j ACCEPT
```
Allow forwarding traffic:
```bash
iptables -A FORWARD -i wlp3s0 -o vmbr0 -d 10.10.10.0/24 -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
```

###### Give VMs DHCP

By using `dnsmasq` :

Edit:
```shell
nano /etc/dnsmasq.d/proxmox-vm.conf
```
Add:
```vim
interface=vmbr0
bind-interfaces

dhcp-range=10.10.10.100,10.10.10.200,255.255.255.0,12h

dhcp-option=3,10.10.10.1
dhcp-option=6,10.10.10.1

server=1.1.1.1
server=8.8.8.8
```
Then:
```shell
systemctl restart dnsmasq
```
Then:
```shell
systemctl enable dnsmasq
```

Then check everything:
```
iw dev
```
and:
```
iw dev wlp3s0 link
```

###### Changing Proxmox Host IP to Wi-Fi Interface

Edit:
```shell
nano /etc/network/interfaces
```
To:
```
auto lo
iface lo inet loopback

auto wlp3s0
iface wlp3s0 inet static
    address 192.168.1.69/24
    gateway 192.168.1.1
    wpa-conf /etc/wpa_supplicant/wpa_supplicant-wlp3s0.conf

auto vmbr0
iface vmbr0 inet static
    address 10.10.10.1/24
    bridge-ports none
    bridge-stp off
    bridge-fd 0
    
        post-up   echo 1 > /proc/sys/net/ipv4/ip_forward
        post-up   iptables -t nat -A POSTROUTING -s '10.10.10.0/24' -o eno1 -j MASQUERADE
        post-down iptables -t nat -D POSTROUTING -s '10.10.10.0/24' -o eno1 -j MASQUERADE    

iface nic0 inet manual
```

Apply configuration:
```shell
ifreload -a
```

Login to `192.168.1.69:8006` via web browser to access Proxmox Host.

The current System architecture would be:
```
                       Internet
                           │
                    ┌──────┴──────┐
                    │ Wi-Fi Router│
                    │ 192.168.1.1 │
                    └──────┬──────┘
                           │
                      Wi-Fi (WPA)
                           │
	                     wlp3s0
	                  192.168.1.69/24
                           │
                  ┌────────┴────────┐
                  │     Proxmox     │
                  │      Host       │
                  │                 │
                  │ IP forwarding   │
                  │ NAT / iptables  │
                  └────────┬────────┘
                           │
                        vmbr0
                      10.10.10.1/24
                           │
                ┌──────────┼──────────┐
                │          │          │
              VM 201     VM 202     VM 203
            10.10.10.x  10.10.10.x  10.10.10.x
                │          │          │
                └──────────┴──────────┘
                           │
                        dnsmasq
                       DHCP + DNS
```

Note that `192.168.1.0/24` is the physical/home network and `10.10.10.0/24` is the VM/private network.

### Setting up Proxmox

We need to make sure that Proxmox can have updates. 

Go to [PVE Post Install Script](https://community-scripts.org/scripts/post-pve-install) and copy the script provided.

Paste the script onto the terminal of the Proxmox.

##### Qemu-Guest Agent

The qemu-guest agents is a helper daemon used to exchange information between the host and the guest, and to execute command in guest.

```bash
apt-get install qemu-guest-agent
```

