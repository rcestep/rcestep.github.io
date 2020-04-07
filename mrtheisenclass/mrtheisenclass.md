## Mr. Theisen's Classes
-------------------------

The networking track classes at Mitchell are mainly taught by Mr. Theisen and with his teaching, I was able to learn so much about network administration and how to setup, monitor, troubleshoot, and administer large enterprise networks.  With his guidance, I have learned about networking concepts like switching and routing, the OSI model for troubleshooting, the routing protocols of networks and the internet and much more.  The classes challenged me to get better with each lab I did.  I learned and mastered Cisco IOS for switches and routers and even though I may have my blank moments, I can get the job done in the end.

Some of the configurations I have done on Cisco Switches are applying VLANs

```
vlan 10
  name IT
vlan 20
  name HR
vlan 30
  name DEVOPS
vlan 40
  name MANAGEMENT
vlan 99
  name Native
```

Doing the VLANs, issuing the **switchport mode access** and **switchport mode trunk** commands allowed for VLAN trunking between switches or trunking to a router.  For example:

```
int range f0/1-8
  switchport mode access
  switchport access vlan 10
int range f0/9-16
  switchport mode access
  switchport access vlan 20
int range f0/17-24
  switchport mode access
  switchport access vlan 30
int g0/1
  switchport mode trunk
  switchport trunk allowed vlan 10,20,30
  switchport trunk native vlan 99
```

Once the switches are configured with VLANs, you can go into the router and make sure that sub-interfaces are configured on the router interface facing the switch.

```
int g0/0
  no shutdown
int g0/0.10
  encapsulation dot1q 10
  ip address 192.168.10.1 255.255.255.0
  no shutdown
int g0/0.20
  encapsulation dot1q 20
  ip address 192.168.20.1 255.255.255.0
  no shutdown
int g0/0.30
  encapsulation dot1q 30
  ip address 192.168.30.1 255.255.255.0
  no shutdown
int g0/0.1000
  encapsulation dot1q 99
  ip address 192.168.99.1 255.255.255.0
  no shutdown
```

These configurations would be necessary to setup what is called Inter-VLAN routing and this specific type is called Router-on-a-Stick because traffic is being trunked on one physical interface.

There are many more configurations that I could showcase here and I am positive that if I did, this portfolio would become a book, so I will leave it at that, but this is exactly the type of knowledge that I have acquired at Mitchell, and it is with this training that I will be able to work in the IT field and be able to excel in ways that I cannot even fathom!

I also learned about setting up Windows Server to support company's in a way to allow many other workers in many different settings to efficiently do their work as well.  Setting up a domain controller was at first very challenging, but with practice, I was able to get that skill down as well.  With the training that I acquired from Mitchell, I can support company’s' infrastructures and manage not only the network equipment like switches and routers but also servers and clients.  I have learned about client-server relationships and how a client accesses information and resources using a central server that is hosting everything that a client would need to properly function.  Using a DC that is hosting a file server and using Group Policy to dictate how the machine operates, clients can be fine-tuned to perform how the company needs them to perform.

[Go back to Home](https://rcestep.github.io)

[LinkedIn](https://linkedin.com/in/roland-c-estep) | [GitHub](https://github.com/rcestep) | [Discord](https://discordhub.com/profile/532348150019522580)
-------------------------------------------------- | ------------------------------------ | ------------------------------------------------------------
Email: **roland.estep@outlook.com**                | Phone: **(980)892-2512**             |
