
## Table of Contents
- [Specify Trusted Systems](#DNS_Defenses_Trust)
    - [Verify, Verify, Verify](#DNS_Defenses_Trust_verify)
    - [Engage with Project Community](#DNS_Defenses_Comm)
    - [Restrict Lines of Communication](#DNS_Defenses_Comm)
- [Monitoring](#DNS_Defenses_Mon)
    - [Traffic Monitoring](#DNS_Defenses_Mon_traffic)
    - [Chain Metadata](#DNS_Defenses_Mon_meta)


### Introduction
To make something 100% secure, unplug it and turn it off.  However, there are some things you could do:

<a id="DNS_Defenses_Trust"></a>
### Specify Trusted Systems
Try to create a list of systems/services that are trusted, these services would range from:
+ DNS Servers - (Query DNS Seeds).
+ Full Nodes - (Establish A Connection).
+ Hosting Server/Environment (Got To Live Somewhere)

If there is no trusted list, there are some things you can do to give yourself peace of mind:

<a id="DNS_Defenses_Trust_verify"></a>
**Verify, Verify, Verify**

Where possible, check the official website and documentation, they will generally contain all the information you require.  This includes IP's, URL's and even SHA1 hashes of binaries/downloads.  

The information you are about to act on, does it match up? Is it safe?

<a id="DNS_Defenses_Trust_community"></a>
**Engage with Project Community**

Join and communicate with the project community, from past experience they are very friendly places.  They will be able to advise on which IP's are `Officially` hosting services; giving more insight into both the project and blockchain technology.

<a id="DNS_Defenses_Comm"></a>
**Restrict Lines of Communication**

Does the node/application/server need unrestricted outbound access to the local network or internet?  Who do you really want the server to talk to for information?

There are a number of things that you can do to restrict comms:
+ Tunnel Traffic Through a Proxy (where possible)
+ Restrict (at the network layer) to Trusted Hosts Only (e.g. Only Permit DNS to 8.8.8.8)
+ Hardcode DNS Entries 
  + On Server (`/etc/hosts`) - This is not ideal, doesn't scale
  + Locally Controlled DNS
+ Hardcode Trusted Nodes/Peers In Node Config File.

<a id="DNS_Defenses_Mon"></a>
### Monitoring
There are possible ways in order to detect whether an attack is being performed, these include:

<a id="DNS_Defenses_Mon_traffic"></a>
**Traffic Monitoring**

An attacker attempting to perform a man-in-the-middle (MiTM) attack will send numerous ARP/DNS/Other packets at the system.  Some of the following should assist in detecting such an attack:

+ Intrusion Detection System (IDS) (e.g. Snort[^111])

<a id="DNS_Defenses_Mon_meta"></a>
**Chain Metadata**

Should your tin-foil hat be rightfully on, it could be possible to verify your node is connected to the correct network and is receiving the correct data. This can be done by using any number of data points that are accessible on the network:

+ Block Height (Fork Detection)
  + Official Explorer
  + Query Externally Trusted Nodes
+ Client Versions


[^111]: Snort Website
  https://www.snort.org/