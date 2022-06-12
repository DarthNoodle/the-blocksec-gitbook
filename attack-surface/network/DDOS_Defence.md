# Table of Contents
+ [Blockchain Mitigations](#DDOS_Def_Mit)
    + [##Topology](#DDOS_Def_Mit_topology)
        + [##High Availability](#DDOS_Def_Mit_highavail)
        + [##Hide/Obfuscate Validators](#DDOS_Def_Mit_hidevalidators)
    + [##Communication](#DDOS_Def_comm)
        + [##Project Team](#DDOS_Def_comm_team)
        + [##Community](#DDOS_Def_comm_community)
    + [##Backup Keys](#DDOS_Def_keys)
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
    + [##Caching](#DDOS_Def_StdMit_Caching)
    + [##DDOS Provider](#DDOS_Def_StdMit_DDOSProvider)
+ [##Monitoring & Alerting](#DDOS_Def_Monitoring)
    + [##Network Traffic](#DDOS_Def_Monitoring_NetworkTraf)
    + [##Chain Traffic](#DDOS_Def_Monitoring_ChainTraf)

# Introduction
Attacks such as Denial of Service (DoS) can be very difficult to prevent in its entirety; in general, these attacks consist of multiple compromised systems which can bring large amounts of traffic to bare with very little cost to themselves.  On the other hand, defending against such attacks can require a significant amount of resources and can prove to be quite costly from both a time (man hours) and monetary perspective.  However,  there are some steps/controls that project teams could take in order to reduce the opportunity and susceptibility for DoS attacks [^6].


<a id="DDOS_Def_Mit"></a>

# Blockchain Mitigations

<a id="DDOS_Def_Mit_topology"></a>

## Topology

<a id="DDOS_Def_Mit_highavail"></a>

### High Availability
+ make sure validators

<a id="DDOS_Def_Mit_hidevalidators"></a>

### Hide/Obfuscate Validators
+ where possible hide validators
    + cosmos sdk example

<a id="DDOS_Def_comm"></a>

## Communication

<a id="DDOS_Def_comm_team"></a>

### Project Team
+ OOB Comms (e.g. whatsapp)

<a id="DDOS_Def_comm_community"></a>

### Community
+ Ensure multiple announcement mediums
    + Discord
    + Website
    + Twitter
    + Telegram
    + Network Broadcast

<a id="DDOS_Def_keys"></a>

## Backup Keys
+ Can easily nuke and spin up another validator
+ prevents attacks targeting the key storage/retrieval










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

<a id="DDOS_Def_StdMit_DDOSProvider"></a>
## DDOS Provider



<a id="DDOS_Def_Monitoring"></a>

# Monitoring & Alerting

<a id="DDOS_Def_Monitoring_NetworkTraf"></a>

## Network Traffic
+ similar to DNS section

<a id="DDOS_Def_Monitoring_ChainTraf"></a>

## Chain Traffic
+ detect conditions such as:
    + high gas fees
    + mempool congestion
    + block times




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