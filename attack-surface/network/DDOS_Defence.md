# Table of Contents
+ [Blockchain Mitigations](#DDOS_Def_Mit)
    + [Topology](#DDOS_Def_Mit_topology)
        + [High Availability](#DDOS_Def_Mit_highavail)
        + [Hide/Obfuscate Validators](#DDOS_Def_Mit_hidevalidators)
          + [TOR/ Onion Network](#DDOS_Def_Mit_hidevalidators_TOR)
          + [VPN Providers](#DDOS_Def_Mit_hidevalidators_VPN)
          + [Sentry Nodes](#DDOS_Def_Mit_hidevalidators_Sentry)
    + [Communication](#DDOS_Def_comm)
        + [Project Team](#DDOS_Def_comm_team)
        + [Community](#DDOS_Def_comm_community)
+ [Standard Mitigations](#DDOS_Def_StdMit)
    + [Rate Limiting](#DDOS_Def_StdMit_RateLimit)
        + [Ingress Data Limit](#DDOS_Def_StdMit_RateLimit_Ingress)
        + [Total Connections/Users](#DDOS_Def_StdMit_RateLimit_Conn)
        + [Configure Timeouts](#DDOS_Def_StdMit_RateLimit_Timeout)
    + [Restrict Access](#DDOS_Def_StdMit_RestrictAccess)
        + [Whitelists](#DDOS_Def_StdMit_RestrictAccess_Whitelist)
        + [Blacklists](#DDOS_Def_StdMit_RestrictAccess_Blacklist)
        + [Blacklist vs Whitelist](#DDOS_Def_StdMit_RestrictAccess_vs)
    + [CDN](#DDOS_Def_StdMit_CDN)
    + [Load Balancing](#DDOS_Def_StdMit_LoadBalance)
    + [Caching](#DDOS_Def_StdMit_Caching)
    + [DDOS Provider](#DDOS_Def_StdMit_DDOSProvider)
+ [Monitoring & Alerting](#DDOS_Def_Monitoring)
    + [Network Traffic](#DDOS_Def_Monitoring_NetworkTraf)
    + [Chain Traffic](#DDOS_Def_Monitoring_ChainTraf)

# Introduction
Attacks such as Denial of Service (DoS) can be very difficult to prevent in its entirety; in general, these attacks consist of multiple compromised systems which can bring large amounts of traffic to bare with very little cost to themselves.  On the other hand, defending against such attacks can require a significant amount of resources and can prove to be quite costly from both a time (man hours) and monetary perspective.  However,  there are some steps/controls that project teams could take in order to reduce the opportunity and susceptibility for DoS attacks [^6].


<a id="DDOS_Def_Mit"></a>

# Blockchain Mitigations
This section focuses on web3 (blockchain-enabled or focused) technologies.

<a id="DDOS_Def_Mit_topology"></a>

## Topology
The topology of a network/ecosystem can be critical in ensuring efficient day-to-day operations.  Should there be not enough resiliency designed into the solution; attackers could exploit these weaknesses and possibly impact the availability of core/critical services [^13].  Possibly resulting in users  leaving the project/ecosystem.

<a id="DDOS_Def_Mit_highavail"></a>

### High Availability
High Availability (HA) is an operational characteristic where the goal is to ensure a level of operation remains active for higher than normal [^12].  An example would be to ensure the projects Validators are HA, this means the project will attempt to keep them online regardless of what conditions the network is facing.

The goal is to identify single points of failure or areas that could negatively impact the availability of the project.  

Project teams should ask themselves the following questions:

+ Where are my critical resources? (e.g. Seed nodes/Validators/JSON-RPC)
+ How Many Instances Are There?

Once potential failure points have been identified, teams could employ standard HA practices.  Entire books have been written on this subject so the author is going to provide some links for the reader to pursue [^14] [^15].


<a id="DDOS_Def_Mit_hidevalidators"></a>

### Hide/Obfuscate Validators
Validators are a critical, block producing resource that should be available/online as close to 100% of the time.  Should enough validators (33% or more) be taken offline/impacted then there is a very real possibility of the affected network not achieving consensus; halting or taking control of the network [^18].

Validators can be identified through simple things such as information leakage from services or even querying the blockchain and enumerating the information from active nodes [^20] [^21].

Some things that could be done to assist in protecting validators:

<a id="DDOS_Def_Mit_hidevalidators_TOR"></a>

#### TOR/ Onion Network
TOR is an Onion network that is most commonly referred to as "The Darknet", this is an encrypted anonymously routed network where the goal is to browse and access resources anonymously [^19].  It could be possible to host/run a node on this service to provide an additional layer of anonymity/protection.


<a id="DDOS_Def_Mit_hidevalidators_VPN"></a>

#### VPN Providers
Virtual Private Networks (VPN) work on a client-server model where VPN clients are able to connect to a remote VPN endpoint and then tunnel all network traffic (which is encrypted) through the remote endpoint.  This gives the advantage of VPN clients assuming the IP and geographical location of the VPN server. 

Validator and node owners could take advantage of this technology to bypass geographical restrictions or hide their source IP address.

**NOTE:** You may have issues with Network Address Translation (NAT) when attempting to bind ports on external IP's.

<a id="DDOS_Def_Mit_hidevalidators_Sentry"></a>

#### Sentry Nodes
Should your chain technology support it then there are additional, more supported ways in which to protect your validators.  

Within the COSMOS SDK there are concepts known as "Sentry Nodes", these Nodes act as relayers/routers of network traffic both to and from a validator.  This gives the advantage of providing a protective layer around network validators; reducing their overall attack surface.  There are a number of different ways in which this can be employed, for a good overview of the different compositions, please refer to this link [^22].

<a id="DDOS_Def_comm"></a>


## Communication
Communication is critical when it disruptions occur, if project team members cannot communicate then their ability to coordinate and respond effectively would be greatly hampered. 


<a id="DDOS_Def_comm_team"></a>

### Project Team
The project team is also a critical component where steps should be taken to ensure multiple lanes of communication are available to each other in the event of an outage/disruption.  

Depending on the level of trust, it is generally recommended that projects have at least one Out of Band (OOB) methods of communication in conjunction to the primary means.

Examples of Primary Methods:
+ Discord Server
+ Telegram Channel 

Examples of Secondary Methods:
+ Direct Messaging Apps (e.g. WhatsApp / Signal)
+ Email
+ Mobile Phone Numbers


<a id="DDOS_Def_comm_community"></a>

### Community
Should an outage or disruption occur then keeping the community well informed with status updates is also crucial, while the majority of users will be clustered around the primary means of communication (e.g. the project Discord server).  How do you keep them notified if the primary comms go down?

Project teams should consider updating their FAQ (or similar) channels to outline additional sites/sources where information can be found in the event of an outage.  Teams should also consider setting up a playbook (e.g. this is what we do when X happens) in order to ensure this process is as smooth and reactive as possible.

Some examples of additional forms of notification/communication:
+ Project Website
+ Twitter
+ Network Broadcast (similar to BTC Alert [^16])
+ Telegram


<a id="DDOS_Def_StdMit"></a>

# Standard DOS Mitigations
The various options discussed below are generally applied to traditional web2 type infrastructure, however it is still relevant for the various web3 blockchain enabled technologies.

<a id="DDOS_Def_StdMit_RateLimit"></a>

## Rate Limiting
Most attacks are unauthenticated or involve large amounts of redirected traffic, rate limiting provides a process in which to control the rate of traffic both to and from a resource (such as an API or JSON-RPC service).

It is possible to implement rate limiting at various levels of the tech stack; ranging from application down to the network later.  In conjunction it could also be based on numerous data points and imposed constraints.

An example of some of these datapoints and areas where controls can be implemented are outlined below, it should be noted that this is not a comprehensive list and is meant to give the reader an idea [^1]:

<a id="DDOS_Def_StdMit_RateLimit_Ingress"></a>

### Ingress Data Limit

Permit a maximum limit of requests over a given time period (e.g. 2 requests a second). Once limit is reached, drop all connections.

NOTE: Do not set threshold too low as you could impact legitimate clients, investigate logs and other data capture sources to determine an appropriate limit.

<a id="DDOS_Def_StdMit_RateLimit_Conn"></a>

### Total Connections/Users

Specify the total number of users/connections that are permitted to access a resource at any given time.  The higher the limit, the more resources that would be required.

<a id="DDOS_Def_StdMit_RateLimit_Timeout"></a>

### Configure Timeouts

Where possible, configure a timeout for any clients/connections/resources that are idle; such connections take up resources which could be used to service others.

Consideration should also be given to implementing an absolute timeout where connections can only stay "established" for a maximum amount of time.  After which, they have to reconnect.

<a id="DDOS_Def_StdMit_RestrictAccess"></a>

## Restrict Access

Is the resource meant to be accessed publicly or are there a smaller subset of users (e.g. project team members or employees/VIPs)?  Restricting access to trusted, known IP addresses could greatly reduce the scope an attacker can utilise when targeting your resources.

There are two main methods which can be applied:

<a id="DDOS_Def_StdMit_RestrictAccess_Whitelist"></a>

### Whitelists

Whitelists are like "Bouncers" you see on the door to venues; If your not on the list, your not getting in!  Should access be restricted to a known quantity (e.g. group of individuals) then this information can be used to check whether they are permitted access[^3].

Data that could be used for a whitelist could be:
+ IP Addresses
    + From a Privileged Access Workstation (PAW) / JumpBox
    + Corporate IP Addresses
+ Account Details
    + Username
    + Wallet/Contract Address

In the form of `bitcoind` an example implementation[^2] could be to use `rpcallowip` which only permits specified IP's access.

<a id="DDOS_Def_StdMit_RestrictAccess_Blacklist"></a>

### Blacklists

Blacklists are the opposite of whitelists; the whitelist contained trusted sources, however the blacklist contains non-trusted resources.  So, using the same bouncer context, if your ON the list, your NOT getting in.  This approach is not as efficient as whitelisting and is contrasted in the section below.  This approach can be applied to publicly facing resources where everyone is meant to have access [^3].

Data that could be used for blacklists are:

+ IP Addresses
    + Known Malicious IP Lists (Google `Malicious IP List`)
    + Geolocation
+ Account Details
    + Username
    + Wallet/Contract Address

<a id="DDOS_Def_StdMit_RestrictAccess_vs"></a>

### Blacklist vs Whitelist

Both approaches have their pro's and con's, for an more detailed overview please see this resource [^3].  Which one to use generally depends on what the perceived risks are and how the resources are accessed.

Where possible, whitelists would be considered the better approach because the listed resources are trusted.  Effort would be required in identifying all trusted sources, however once completed no further action would be required (unless you add/update/delete items).  A blacklist only contains KNOWN BAD and must be constantly updated in order to keep the list relevant, it does not protect the UNKNOWN BAD from accessing the resource; giving an attacker a larger range of scope.

<a id="DDOS_Def_StdMit_CDN"></a>

## CDN
Content Delivery Networks (CDN) is a group of servers that are distributed throughout the world; these servers contain copies of "website content" (e.g. images/ HTML / CSS) so they are not only stored on your hosting server.

Why do this? CDN's are designed for high-bandwidth access and attempt to be closer to users (globally) than just your hosting platform; this allows for quicker user access and distributing (traffic) loads.

When an attacker performs a DDOS attack against your project, they could target the hosting webserver; if the UI isn't working, users will leave even if the underlying blockchain is still operational.  Should a CDN server become overloaded, they will automatically route traffic to an alternate server without having any impact on your original hosting resource.  Further to this, most CDN's provide caching and DDOS capabilities which could be of benefit to the project team [^4].



<a id="DDOS_Def_StdMit_LoadBalance"></a>

## Load Balancing
Load Balancers (LB) are a resource that is able to spread the workload/tasks over multiple systems with the aim of making overall processing and responsiveness more efficient. This allows all resources to be used instead of overloading some resources while others sit idle and also provide the benefit of increased uptime/availability.  With the load being spread between multiple resources, there is less likelihood resources such as servers and links become exhausted[^6].

Some load balancers also have additional capabilities such as [rate limiting](#DDOS_Def_StdMit_RateLimit) and even simple IDS/IPS capabilities [^5]. 

Consideration should be given to placing LB's in front of critical resources such as a validator, if there are no capabilities for key sharing or similar.  The project team could run foul of malicious behaviour protections which could result in actions such as `Slashing` [^7].


<a id="DDOS_Def_StdMit_Caching"></a>

## Caching

Caching can be performed at many different layers (such as CDN through to Database and Web/API Response) within the technology stack.  So, what is caching exactly?

Querying data from computationally expensive sources can be slow and resource intensive.  Caching attempts to increase the speed/efficiency of these responses by storing frequently accessed data in memory or other high-speed, low latency/resource mediums (such as memory) [^8]. 

Attackers attempting to starve their target of resources would attempt to access computationally expensive resources (e.g. hitting a query API repeatedly).  By caching the response, the underlying resources (such as a Database or Node) wont even be queried; further reducing the attack surface and raising the DOS difficulty bar.


<a id="DDOS_Def_StdMit_DDOSProvider"></a>

## DDOS Provider

Distributed Denial of Service (DDOS) providers are companies that specialise in providing DOS mitigation services [^9].  Such services would include a wide range of functionality/controls, most of which is outlined in the above sections.

A project team should seriously considering utilising professional DDOS providers for their production environments and/or critical services in order to ensure the maximum amount of availability possible.



<a id="DDOS_Def_Monitoring"></a>

# Monitoring & Alerting
Monitoring for and detecting DOS attacks is crucial to ensuring normal operation of projects. The methods and/or processes used tend to vary depending on the teams level of risk, availability and resources.


<a id="DDOS_Def_Monitoring_NetworkTraf"></a>

## Network Traffic
The majority of web2 (non-blockchain) DOS attacks are network or application based, as such it could be possible to utilise OpenSource tools [^10] to listen and detect for attacks.

Such tools would listen for [^11]:

+ TCP/UDP/ICMP Flooding
+ DNS Flooding
+ Application Based (e.g. HTTP)


<a id="DDOS_Def_Monitoring_ChainTraf"></a>

## Chain Traffic

What about web3 (blockchain-enabled) technologies, while it could be possible to monitor network traffic.  Consideration should be given to investigating what metrics can be obtain from on-chain data; this could provide other indicators of DOS based attacks.

Some possible areas to investigate and monitor would include:

+ High GAS Fees
+ High Memory Pool Congestion 
+ Block times deviate from their median (e.g. BTC 1 block every 10 mins).





[^1]: OWASP: Rate Limiting
https://cheatsheetseries.owasp.org/cheatsheets/Denial_of_Service_Cheat_Sheet.html#rate-limiting
[^2]: Stack Exchange - Bitcoin JSON RPC not working on Remote IP
  https://bitcoin.stackexchange.com/questions/91274/bitcoin-json-rpc-not-working-on-remote-ip
[^3]: Whitelisting explained: How it works and where it fits in a security program
  https://www.csoonline.com/article/3562429/whitelisting-explained-how-it-works-and-where-it-fits-in-a-security-program.html
[^4]: Presentation: Best Practices for Using CDNs Against DDoS Attacks  (By Wilson Rogério Lopes)
  http://slides.lacnic.net/wp-content/uploads/2017/09/cdn-ddos-wilson-lopes-v2.pdf
[^5]: Use a Load Balancer as a First Row of Defense Against DDOS
  https://www.haproxy.com/blog/use-a-load-balancer-as-a-first-row-of-defense-against-ddos/
[^6]: AWS Best Practices for DDoS Resiliency
  https://docs.aws.amazon.com/whitepapers/latest/aws-best-practices-ddos-resiliency/welcome.html
[^7]: How to avoid getting slashed
  https://www.coinbase.com/cloud/discover/solutions/dont-get-slashed
[^8]: Caching Overview
  https://aws.amazon.com/caching/
[^9]: Top 8 DDoS Protection Service Providers for 2022
  https://www.esecurityplanet.com/products/distributed-denial-of-service-ddos-protection-vendors/
[^10]: Snort IDS
  https://www.snort.org/
[^11]: 5 Items to Monitor to Detect DDoS Attacks
  https://www.nextgov.com/ideas/2021/08/5-items-monitor-detect-ddos-attacks/184874/
[^12]: Wikipedia: High Availability
[^13]: A multi-tiered DDoS protection architecture
  https://www.f5.com/services/resources/white-papers/the-f5-ddos-protection-reference-architecture
  https://en.wikipedia.org/wiki/High_availability
[^14]: AWS Well-Architected Framework
  https://d1.awsstatic.com/whitepapers/architecture/AWS_Well-Architected_Framework.pdf
[^15]: Making the Most of AWS High Availability Architecture for Enterprise Workloads
  https://cloud.netapp.com/blog/aws-high-availability-architecture
[^16]: Bitcoin Wiki: Alert System
  https://en.bitcoin.it/wiki/Alert_system
[^17]: Intro to Ethereum Staking and Validators
  https://blockdaemon.com/platform/validator-node/ethereum-introduction/ 
[^18]: What is Byzantine Fault Tolerance? Quick intro to PBFT for Crypto
  https://medium.com/geekculture/what-is-byzantine-fault-tolerance-quick-intro-to-pbft-for-crypto-4b54ce70ecde
[^19]: What Is Tor and Why Should I Use It?
  https://lifehacker.com/what-is-tor-and-should-i-use-it-1527891029
[^20]: Running Bitcoin & Lightning Nodes Over The Tor Network (2021 Edition)
  https://stopanddecrypt.medium.com/running-bitcoin-lightning-nodes-over-the-tor-network-2021-edition-489180297d5
[^21]: How To Sync an Ethereum Node via Tor
  https://medium.com/@oaeee/how-to-sync-an-ethereum-node-via-tor-755534775ae1
[^22]: Playbook For Cosmos Validators: Node Architecture Choices
  https://medium.com/@kidinamoto/tech-choices-for-cosmos-validators-27c7242061ea