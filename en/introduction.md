# Building a Professional Network 🌐

In this repository, I will guide you on how to build a practical professional network! Additionally, I'll provide some tips on attack and defense in securing your network.

Let's get started!
-----------

Well, let's say you have two computers and want to establish communication between them. For this, each one needs a "unique" address so they can send messages to each other! We'll call this address the **MAC address**.

Technically, the MAC address is a unique alphanumeric sequence represented by six pairs of numbers and letters, separated by colons (e.g., `00:1A:2B:3C:4D:5E`). Each network device manufacturer is assigned a unique set of identifiers, known as the **OUI (Organizationally Unique Identifier)**, which is part of the MAC address. This means that the first three pairs of the MAC address identify the specific manufacturer of the device.

To bridge the gap between these two devices, a **switch** is necessary. It works like this: "Hey switch, this is my MAC address, and this is the MAC address of the recipient, figure it out!" The switch compares it with the table and determines the recipient's port.

(!) **Note**: A broadcast storm can occur in networks with switches interconnected by two different cables when there is a loop in the network topology. It's important to configure switches with a loop prevention protocol, such as the **Spanning Tree Protocol (STP)**.

------

But MAC addresses have a drawback. When you decide to change equipment, you'll need to reconfigure everything with the new address. To solve this, we have IP addresses.

**IPv4** (e.g., `192.168.1.1`):
- Composed of 32 bits, divided into four octets.
- Each octet is represented by a decimal number from 0 to 255.
- Faces address scarcity due to the increasing number of devices connected to the internet.

**IPv6** (e.g., `2001:0db8:85a3:0000:0000:8a2e:0370:7334`):
- Composed of 128 bits, expressed in hexadecimal notation.
- Developed to overcome IPv4 address scarcity, providing a virtually unlimited number of IP addresses.

Just like the MAC address, if the IP address is static, every time a new machine enters the scene, you'll have to tweak the entire configuration. For this, we have the **DHCP protocol**, which dynamically assigns addresses to each device.

----------------------

Most of the time, you'll connect to a hostname, and your computer will ask the DNS server: "Hey, who has this hostname?" The DNS functions as a name-to-address translation system. When you type a domain name in your browser, the computer sends a request to a DNS server.

**DNS**:
- Functions as a name-to-address translation system.
- When you type a domain name, the computer sends a request to a DNS server.

**ARP (Address Resolution Protocol)**:
- ARP functions as a local "phone book" for the network.
- If a computer knows the IP address of another but doesn't know the corresponding MAC address, it sends an ARP request to find out.

**ARP**:
1. ARP Request:
   - A device on the network issues an ARP Request to discover the MAC address associated with a specific IP address.
   - The request is sent to all devices on the local network.

2. ARP Reply:
   - The device with the corresponding IP address responds with its ARP information.
   - The ARP reply contains the MAC address associated with the sought IP address.

3. ARP Table Updates:
   - The requesting device updates its local ARP table with the newly discovered IP and MAC address pair.

4. ARP Cache:
   - To avoid constant repetition of the process, many devices maintain an "ARP cache."

---------

## But what if you want to communicate with "google.com," for example? We have forwarding servers and routers!

- A forwarding server allows you not to have all domain names locally in your network.

- **Routers** are essential. When the DHCP client sends the IP address of your device, it also sends a default gateway. Your computer will look at Google's address and say, "Wow, this address is very different from mine... so I won't do what I usually do. I'll just grab my default gateway, get its MAC address, and send this packet to the router, and let it handle it!"

- I tried to summarize it in the simplest way so that you can follow this journey without too many doubts. I hope you enjoyed the content!
