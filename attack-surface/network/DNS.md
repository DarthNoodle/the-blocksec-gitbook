# Domain Name Services (DNS)
### Table of Contents
1. [DNS Overview](#DNS-Overview)
2. [DNS Seed Nodes](#DNS_SeedNodes)



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


[^1]: Google: General DNS Overview
  https://cloud.google.com/dns/docs/dns-overview
[^2]: Bitcoin Developer Guide
  https://btcinformation.org/en/developer-guide#p2p-network
[^3]: Bitcoin DNS Seed List
  https://en.bitcoin.it/wiki/Satoshi_Client_Node_Discovery#DNS_Addresses
