# Networking Fundamentals

1. The LOOPBACK interface is what allows a system to communicate with itself. localhost 
    This is the lo device. 
2. The other network device on teh system is an actual hardware device is the eth0. 

3. We can use the ifconfig tool or the ip command. 

4. a host is a device with an ip address. this is readable name for an ip address (dns)

## DNS 

- FQDN = 
    fully qualified domain name. contiains a domain name and a top level domain name
    webprod01.mycompany.com
- TLD = 
    .com, .net,.org, etc.
- Domains = 
    to the left of the TLD.
- Subdomain = 
    to the left of the Domains.


Dispalying the hostname:
```
hostname
uname -n 
hostname -f = shows the FQDN
```

Setting the hostname on ubuntu or redhat systems.
```
hostname <name>
echo '<name>' > /etc/hostname
```

For earlier versions of linux:
```
change the /etc/sysconfig/network
HOSTNAME=<value>
```

Resolving DNS Names:
```
host
dig
```

/etc/hosts is local to the linux system. not to the rest of the network.


/etc/nsswitch.conf file controls the search order for resolutions.
This file controls which file will be searched for in order of operation for DNS utilities and name switch.


## Network Ports 

1. Network Ports:
```
    - When a service starts it binds itself to a port.
    - There are default ports, well known ports: 1-1,023
    - These ports are sudo ports, and require system level permission
```
2. /etc/services file:
```
    - maps port names to port numbers
    - ie. ssh 22/tcp
```
3. DHCP:
```
    - Dynamic Host Configuration Protocol
    - DHCP servers assign IP address to DHCP clients. Assigns IP
      addresses to hosts on a network.
        a. IP Address
        b. netmask
        c. gateway
        d. DNS servers
    - Each IP is "leased" from the poolof IP addresses the DCHP
      server manages. 
 ```   

To configure DHCP:
```
    RHEL - ifconfig -a or ip link
        set BOOTPROTO=dhcp in the: 
            - /etc/sysconfig/network-scripts/ifcfg-DEVICE
            - /etc/sysconfig/network-scripts/ifcfg-eth0 
            - /etc/sysconfig/network-scripts/ifcfg-enp5s2
            
    Ubuntu: /etc/network/interfaces
        set: 
            - auto eth0
            - iface eth0 inet dhcp
```

Assigning a static IP to a linux system: 
```
    RHEL:
        change the /etc/sysconfig/network-scripts/ifcfg-eth0
            BOOTPROTO=static
            Make sure to check the a ONBOOT=yes if we want this 
            to actuate on boot.

    Ubuntu: 
        change the /etc/network/interfaces
            ie
            """
                auto eth0
                iface eth0 inet static
                    address 10.109.155.174
                    netmask 255.255.255.0
                    gateway 10.109.155.1
            """
 ```   
        
Manually assigning an IP address:

Command Format:
ip address add IP[/Netmask] dev <Network_interface>

```
ip address add 10.11.12.13 dev eth0
ip address add 10.11.12.13/255.255.255.0 dev eth0
ip link set eth0 up 
```

or 

```ifconfig <network interface> <addr> netmask <subnetmask>```

```
ifconfig etho0 10.11.12.13 netmask 255.255.255.0
ifconfig eth0 up
```
    
### ifup/ifdown 

these commands can be used to bring a network up or down.
```
ifup eth0
ifdown eth0
```

### networking troubleshooting ###

1. Ping
2. traceroute/ tracepath
3. netstat
4. tcpdump
5. telnet


    

