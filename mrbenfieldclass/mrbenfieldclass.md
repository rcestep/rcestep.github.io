## Mr. Benfield's Class
-------------------------

I had a **great honor** to attend the Security class being led by Mr. Benfield.  His wisdom and many real-life examples of security breaches that he knew of or had experienced really helped me to learn one thing: security is an ongoing process that should be tended to with care and with great importance!  Learning about the different attack types and how black hat hackers could potentially cause chaos for many companies with just the stroke of the Enter key!  I learned a lot about network infrastructures and how to set them up in a secure fashion to ensure that maximum security can be attained.  This class we had many labs that had to deal with security and aspects of security and we even had a server that we had to break into.  With the help of my team, we were able to access a Linux server with root privileges by running a Nmap scan and finding a server running a FTP server and able to find a vulnerability in the machine.  We found credentials for a Windows server that had an encrypted password that was all in binary.  Using the key, we used ANDing to decrypt the password and we were able to take the credentials we found to login to the Linux machine with a regular user.  From there, we accessed the /etc/passwd file and edited the user to have root privileges.  The information I learned in that class will always stay with me as I go further with my career.

In addition to that class, I am currently learning more about Cisco ASA firewalls and adding more to my skill bank by configuring ASA firewalls to filter traffic inside and outside an enterprise network.

Some of the configurations are as follows:

```
int g0/0
  nameif inside                                   # Naming the interface is key.
  ip address 192.168.0.1 255.255.255.0
  no shutdown
  exit
int g0/1
  nameif outside                                  # Naming the interface is key.
  ip address 10.0.0.1 255.255.255.252
  no shutdown
  exit
object network INSIDE_LAN                         # Making objects makes configuring access lists easier.
  subnet 192.168.0.0 255.255.255.0
  nat (inside,outside) dynamic interface          # Configuring NAT is on the objects not the interfaces.  The interfaces are specified in the command.
  exit
object network OUTSIDE_WAN
  subnet 10.0.0.0 255.255.255.252
  exit
object network REMOTE_LAN
  subnet 172.16.0.0 255.255.255.0
  exit
object-group SAFE_ICMP
  network-object object OUTSIDE_WAN
  network-object object REMOTE_LAN
  exit
access-list INSIDE extended permit icmp object INSIDE_LAN object-group SAFE_ICMP
access-list OUTSIDE extended permit icmp object-group SAFE_ICMP object INSIDE_LAN
access-group INSIDE in interface inside
access-group OUTSIDE in interface outside
```

These configurations, although hard to read, configure a firewall with IP addresses, labels networks with names, and it allows ICMP traffic from the inside LAN to the remote LAN and the WAN and allows the replies to return as well.  Learning the Cisco ASA configurations have been a challenge, but it's yet another feather in my cap!

Go back to [Home](https://rcestep.github.io)!

[Mr. Cain's Classes](https://rcestep.github.io/mrcainclass/mrcainclass.html)

[Ms. Shoemaker's Classes](https://rcestep.github.io/msshoemakerclass/msshoemakerclass.html)

[Ms. Watt's Class](https://rcestep.github.io/mswattclass/mswattclass.html)

[Mr. Hicks' Classes](https://rcestep.github.io/mrhicksclass/mrhicksclass.html)

[Mr. Theisen's Classes](https://rcestep.github.io/mrtheisenclass/mrtheisenclass.html)

[Mitchell Technological Society](https://rcestep.github.io/mts/mts.html)

[My Oher Accomplishments](https://rcestep.github.io/other/other.html)

[LinkedIn](https://linkedin.com/in/roland-c-estep) | [GitHub](https://github.com/rcestep) | [Discord](https://discordhub.com/profile/532348150019522580)
-------------------------------------------------- | ------------------------------------ | ------------------------------------------------------------
Email: **roland.estep@outlook.com**                | Phone: **(980)892-2512**             |
