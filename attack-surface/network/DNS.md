# Domain Name Services (DNS)
### Table of Contents
1. [DNS Overview](#DNS_Overview)
2. [DNS Seed Nodes](#DNS_SeedNodes)
3. [Attack Vectors](#DNS_Attks)
    - [No Authentication](#DNS_Attks_NoAuth)
    - [DNS Hijacking/Spoofing](#DNS_Attks_Spoofing)
    - [Data Corruption](#DNS_Attks_Corrupt)
    - [Old/Stale Node IPs](#DNS_Attks_OldStale)
    - [Lack of Standards/Controls](#DNS_Attks_Standards)
4. [Defences](#DNS_Attks_Standards)

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

<a name="DNS_Attks"></a>
## Attack Vectors
The client is most at risk during the application start-up phase; it will have no knowledge of the network and as such must find out this information.  DNS seeds are one of the first methods that is attempted to establish a connection to the network.

<a name="DNS_Attks_NoAuth"></a>
#### No Authentication
Blockchain clients rely on the DNS protocol which has no authentication or access controls; meaning it would be difficult for a client to verify the legitimacy of the querying server[^4].

<a name="DNS_Attks_Spoofing"></a>
#### DNS Hijacking/Spoofing
Due to the lack of authentication and encryption/PKI the protocol is susceptible to abuse.  An attacker could poison the DNS server cache or simply trick the user into connecting to a malicious server [^5].

This would permit the attacker to redirect the client to their own malicious nodes; allowing the attacker to feed malicious information about both the blockchain and network state to the client.  This could lead to other attack vectors, such as the `Sybil` attack **(## LINK to Sybil MD ##)**.

<a name="DNS_Attks_Corrupt"></a>
#### Data Corruption
Data corruption from a malicious or corrupt node is a very real possibility that could have an adverse affect on the connecting client.  Depending on how error handling and data verification is implemented, this could lead to either a Denial of Service (DOS) or other possible attack vectors such as remote code execution.

<a name="DNS_Attks_OldStale"></a>
#### Old/Stale Node IPs
DNS Seed nodes in general should dynamically update their connected node list [^2], however some owners maintain a static list.  As such, this list could become old/stale where nodes are no longer available/accessible on those IP addresses.

This could result in a DOS style attack or in a very limited instance, should an attack gain control of the stale IP (which is very unlikely).  They would be able to insert a malicious Seed node into the network.

<a name="DNS_Attks_Standards"></a>
#### Lack of Standards/Controls
Seed nodes are generally operated by the community, as such there may be inconsistencies in both the implementation, configuration and hardening of the seed node and/or DNS provider.

While some efforts have been made to rectify this [^6], is has largely been left to each individual project/community to resolve.  The majority of the time, this area is not addressed and is left unmaintained.

<a name="DNS_Defenses"></a>
## Controls  / Defence
+ Specify Trusted Systems
  + DNS Servers
  + Specify Trusted Nodes
  + FW Rules

+ Monitoring
  + Increased DNS/ARP traffic (spoofing attempts)
  + Monitor local network height/state with other, trusted nodes. (fork detection)



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