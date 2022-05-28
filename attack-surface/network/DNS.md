# Domain Name Services (DNS)
### Table of Contents
1. [DNS Overview](#DNS-Overview)
2. [DNS Seed Nodes](#DNS_SeedNodes)
3. [Attack Vectors](#DNS_Attks)
    - [No Authentication](#DNS_Attks_NoAuth)
    - [DNS Hijacking/Spoofing](#DNS_Attks_Spoofing)
    - [Data Corruption](#DNS_Attks_Corrupt)
    - [Old/Stale Node IPs](#DNS_Attks_OldStale)
    - [Lack of Standards/Controls](#DNS_Attks_Standards)
4. [Defences](#DNS_Attks_Standards)
    - [Specify Trusted Systems](#DNS_Defenses_Trust)
      - [Verify, Verify, Verify](#DNS_Defenses_Trust_verify)
      - [Engage with Project Community](#DNS_Defenses_Comm)
      - [Restrict Lines of Communication](#DNS_Defenses_Comm)
    - [Monitoring](#DNS_Defenses_Mon)
      - [Traffic Monitoring](#DNS_Defenses_Mon_traffic)
      - [Chain Metadata](#DNS_Defenses_Mon_meta)


<a name="DNS_Overview"></a>
## DNS Overview
DNS is a hierarchical, globally distributed database that stores data such as IP addresses that can be queried by a name.  

This allows easily human readable (domain) names to translate to numeric IP addresses used by computers and other devices to communicate with each other [^1].

An example is typing in www.blocksecbook.com into a browser; DNS will convert the URL to an IP address of the web server hosting this site.  The web browser will then attempt to connect directly to the IP address of the web server.

<a name="DNS_SeedNodes"></a>
## DNS Seed Nodes
When a client first starts, it does not have knowledge of the network in order to receive new blocks.  To identify a starting point, the client will perform a DNS query to a pre-determined/hardcoded list of DNS names (called DNS seeds)[^2].

These queries should return DNS A records; containing the IP address of full nodes in which the client can then connect to.

An example is given below[^3]:
```
$ dig @8.8.8.8 seed.bitcoinstats.com a

.. SNIP..

;; ANSWER SECTION:
seed.bitcoinstats.com.  60      IN      A       50.4.210.87
seed.bitcoinstats.com.  60      IN      A       66.85.234.129
seed.bitcoinstats.com.  60      IN      A       72.74.34.120
seed.bitcoinstats.com.  60      IN      A       3.219.41.205
seed.bitcoinstats.com.  60      IN      A       34.235.144.59
seed.bitcoinstats.com.  60      IN      A       158.130.13.32
seed.bitcoinstats.com.  60      IN      A       46.242.91.95
seed.bitcoinstats.com.  60      IN      A       185.44.119.82

.. SNIP ..
```

As can be seen from the above output, a number of FULL nodes IP addresses are listed, a client can now establish a connection with this list and retrieve more network information.  Such as a list of other hosts on the network, the client can then attempt to establish additional connections in order to further increase communication resiliency.

<a id="DNS_Attks"></a>
## Attack Vectors
The client is most at risk during the application start-up phase; it will have no knowledge of the network and as such must find out this information.  DNS seeds are one of the first methods that is attempted to establish a connection to the network.

<a id="DNS_Attks_NoAuth"></a>
#### No Authentication
Blockchain clients rely on the DNS protocol which has no authentication or access controls; meaning it would be difficult for a client to verify the legitimacy of the querying server[^4].

<a id="DNS_Attks_Spoofing"></a>
#### DNS Hijacking/Spoofing
Due to the lack of authentication and encryption/PKI the protocol is susceptible to abuse.  An attacker could poison the DNS server cache or simply trick the user into connecting to a malicious server [^5].

This would permit the attacker to redirect the client to their own malicious nodes; allowing the attacker to feed malicious information about both the blockchain and network state to the client.  This could lead to other attack vectors, such as the `Sybil` attack **(## LINK to Sybil MD ##)**.

<a id="DNS_Attks_Corrupt"></a>
#### Data Corruption
Data corruption from a malicious or corrupt node is a very real possibility that could have an adverse affect on the connecting client.  Depending on how error handling and data verification is implemented, this could lead to either a Denial of Service (DOS) or other possible attack vectors such as remote code execution.

<a id="DNS_Attks_OldStale"></a>
#### Old/Stale Node IPs
DNS Seed nodes in general should dynamically update their connected node list [^2], however some owners maintain a static list.  As such, this list could become old/stale where nodes are no longer available/accessible on those IP addresses.

This could result in a DOS style attack or in a very limited instance, should an attack gain control of the stale IP (which is very unlikely).  They would be able to insert a malicious Seed node into the network.

<a id="DNS_Attks_Standards"></a>
#### Lack of Standards/Controls
Seed nodes are generally operated by the community, as such there may be inconsistencies in both the implementation, configuration and hardening of the seed node and/or DNS provider.

While some efforts have been made to rectify this [^6], is has largely been left to each individual project/community to resolve.  The majority of the time, this area is not addressed and is left unmaintained.

<a id="DNS_Defenses"></a>
## Controls  / Defence
To make something 100% secure, unplug it and turn it off.  However, there are some things you could do:

<a id="DNS_Defenses_Trust"></a>
#### Specify Trusted Systems
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
#### Monitoring
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


[^1]: Google: General DNS Overview
  https://cloud.google.com/dns/docs/dns-overview
[^2]: Bitcoin Developer Guide
  https://btcinformation.org/en/developer-guide#p2p-network
[^3]: Bitcoin DNS Seed List
  https://en.bitcoin.it/wiki/Satoshi_Client_Node_Discovery#DNS_Addresses
[^4]: DNSSEC – What Is It and Why Is It Important?
  https://www.icann.org/resources/pages/dnssec-what-is-it-why-important-2019-03-05-en
[^5]: What is DNS cache poisoning? | DNS spoofing
  https://www.cloudflare.com/en-gb/learning/dns/dns-cache-poisoning/
[^6]: Expectations for DNS Seed operators
  https://github.com/bitcoin/bitcoin/blob/master/doc/dnsseed-policy.md


[^111]: Snort Website
  https://www.snort.org/