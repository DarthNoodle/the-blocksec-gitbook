# Table of Contents
+ [Blockchain Mitigations](#DDOS_Def_Mit)
    + [Topology](#DDOS_Def_Mit_topology)
        + [High Availability](#DDOS_Def_Mit_highavail)
        + [Hide/Obfuscate Validators](#DDOS_Def_Mit_hidevalidators)
    + [Communication](#DDOS_Def_comm)
        + [Project Team](#DDOS_Def_comm_team)
        + [Community](#DDOS_Def_comm_community)
    + [Backup Keys](#DDOS_Def_keys)
+ [Standard Mitigations](#DDOS_Def_StdMit)
    + [Rate Limiting](#DDOS_Def_StdMit_RateLimit)
    + [Restrict Access](#DDOS_Def_StdMit_RestrictAccess)
    + [CDN](#DDOS_Def_StdMit_CDN)
    + [Load Balancing](#DDOS_Def_StdMit_LoadBalance)
    + [Caching](#DDOS_Def_StdMit_Caching)
    + [DDOS Provider](#DDOS_Def_StdMit_DDOSProvider)
+ [Monitoring & Alerting](#DDOS_Def_Monitoring)
    + [Network Traffic](#DDOS_Def_Monitoring_NetworkTraf)
    + [Chain Traffic](#DDOS_Def_Monitoring_ChainTraf)

# Introduction
There are a number of options that could be taken in order to reduce the susceptibility of a Denial of Service (DoS) attack, some of these are outlined below.

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

<a id="DDOS_Def_StdMit_RateLimit"></a>

## Rate Limiting


<a id="DDOS_Def_StdMit_RestrictAccess"></a>

## Restrict Access
+ Blacklists - Akamai?
+ Trusted IPs?

<a id="DDOS_Def_StdMit_CDN"></a>

## CDN
+ Deliver front-end content

<a id="DDOS_Def_StdMit_LoadBalance"></a>

## Load Balancing

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