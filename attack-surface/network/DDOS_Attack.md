## Table of Contents
+ [Are Blockchains DDoS Resistant?](#DDOS_ATTK_Resist)
+ [DDOS Attack Vectors](#DDOS_ATTK)
    + [Number of Block Producing Systems (e.g. Validators)](#DDOS_ATTK_BlockProd)
    + [Start-up Sequences](#DDOS_ATTK_Startup)
    + [Number of Application Interfaces (e.g. JSON-RPC)](#DDOS_ATTK_AppInt)
    + [Site/Resource Hosting](#DDOS_ATTK_Host)
    + [Governance/Management of Critical Resources](#DDOS_ATTK_Govern)
        + [Distribution of Tokens](#DDOS_ATTK_Govern_dist)
        + [Disruption of Voting Processes](#DDOS_ATTK_Govern_vote)
        + [Disruption of Project Admins](#DDOS_ATTK_Govern_admin)
    + [Transaction Throughput](#DDOS_ATTK_TX)
    + [Consensus Delay](#DDOS_ATTK_Cons)
        + [Injection of False/Incorrect Blocks](#DDOS_ATTK_Cons_fblock)
        + [Delay or Increase The Introduction of Blocks](#DDOS_ATTK_Cons_blockdelay)
        + [Target Voting/Consensus Threshold](#DDOS_ATTK_Cons_voting)

<a id="DDOS_ATTK_Resist"></a>
## Are Blockchains DDoS Resistant?
The short answer: **NO**

Well designed and implemented blockchains are distributed in their nature, this is a common misconception.  Yep, nodes/validators are spread out over the world and contain a copy of the ledger.  However, there are many other moving parts of a blockchain ecosystem which must also be factored in to the DDoS equation.

Such parts would be:
+ [Number of Block Producing Systems (e.g. Validators)](#DDOS_ATTK_BlockProd)
+ [Start-up Sequences](#DDOS_ATTK_Startup)
+ [Number of Application Interfaces (e.g. JSON-RPC)](#DDOS_ATTK_AppInt)
+ [Governance/Management of Critical Resources](#DDOS_ATTK_Govern)
+ [Transaction Throughput](#DDOS_ATTK_TX)
+ [Consensus Delay](#DDOS_ATTK_Cons)

Anywhere that has a potential `bottleneck` or `centralisation` in either the process/system/architecture/people can result in a possible Denial of Service (DoS).  Defenders have to identify and map out all possible attack vectors, an attacker only needs to identify one.

<a id="DDOS_ATTK"></a>

## DDOS Attack Vectors
<a id="DDOS_ATTK_BlockProd"></a>

### Block Producing Systems
Block producing systems whether they are miners, validators or order's (HyperLedger) provide a vital role in the blockchain ecosystem.  Without these resources, no new blocks would be produced and as such the network would come to a stop.

Smaller projects are more susceptible to these types of attacks because the networks are generally small in nature; due to the ecosystem being young/immature.  As such the cost of performing such attacks would be much lower to an attacker when compared to attempting to perform a DoS attack on Ethereum.

Some possible attack scenarios would include:
+ Network Traffic Flooding
+ Affecting Traffic Routing (e.g. BGP)
+ Sending Malformed Data
+ Sending Large Volume of Transactions

<a id="DDOS_ATTK_Startup"></a>

### Start-up Sequences
When Nodes/Validators initially start-up they have little to no knowledge of the network [^1].  They will attempt to obtain this knowledge from two places:

+ Locally Provided Configuration Files
+ Connecting To Hard-Coded Network Peers

An example of which is to perform Man-in-The-Middle (MiTM) based attacks [^2] in order to prevent communication with outside resources.  Such an attack would resemble:

+ ARP Spoofing (Routing of Traffic)
+ DNS Hijacking (Change Intended Target)
+ DNS DoS (Unable To Resolve DNS Seed Nodes)

Should the node not obtain any information upon start-up then it would not be able to connect to the network and function as intended.

<a id="DDOS_ATTK_AppInt"></a>

### Application Interfaces
An application interface can be defined as `a service that permits interaction with external users or code`, this means interfaces such as:

+ P2P Protocol (Used To Communicate with other Nodes)
+ JSON-RPC (Web3 Interface, Used By Most Web Apps)
+ gRPC (Less Frequent, Used By Apps)
+ Management (RPC/API Service Used For Remote Admin)

Each of the above listed services run on differing protocols and will have their own nuances with regards to crafting of malicious data/packets.  However, all are susceptible to the  application and network level DoS attack methodologies.

<a id="DDOS_ATTK_Host"></a>
### Site/Resource Hosting
Most Web3 enabled applications consist of lightweight clients (e.g. pure, front-end JavaScript framework apps like Angular/React) which talk directly to Web3 RPC services to both query/receive information.  These lightweight applications do not require much resources to deliver content and can be hosted on cheap VPS systems or similar.  

While these applications are light and can be hosted anywhere, they are still delivered through the standard browser (HTTP(s)) and as such are susceptible to all application and network based DoS attacks.  Should the application be taken offline, the underlying functionality on the blockchain would still work but your average user would not be able to efficiently perform their required actions (when compared to performing the same actions on a web page). 

<a id="DDOS_ATTK_Govern"></a>

### Governance/Management of Critical Resources
Management of the blockchain environment is a critical component and must be protected in order for the blockchain to function.  

Most protocols start life being centrally governed by the project team, once the project has matured to a certain level it is common for a governance token to be used to then control how the project/protocol grows.  This is generally done through ownership of tokens and utilising said tokens to vote on proposals [^5]. As such, attackers constantly probe this area for weaknesses.

<a id="DDOS_ATTK_Govern_dist"></a>
**Distribution of Tokens**

Should the distribution of tokens be heavily skewed/slanted to a particular group or malicious actor; it would be possible for this malicious actor to change how the ecosystem governs.  This could have disastrous consequences for both the integrity and security posture of the network.

An example is the recent Luna SNAFU [^6] where the price of LUNA dropped 99%. It could of been possible for a well-funded malicious attacker to obtain more than 50% of the tokens and as such take control of the network.  The result, the network was stopped.

<a id="DDOS_ATTK_Govern_vote"></a>
**Disruption of Voting Processes**

Communities will generally vote on new proposals that could affect the operation or tokenomics of a project.  It could be possible for attackers to disrupt the process in which users would be able to vote; making the process ineffective.

This could be performed in a number of ways:
+ Target Voting Web Application
+ Explore & Exploit Any Weakness In Voting Contracts
+ Network Congestion (Flood Network)

<a id="DDOS_ATTK_Govern_admin"></a>
**Disruption of Project Admins**

The project team, especially in the early days are critical to the operation of a blockchain network.  Attackers could attempt to disrupt how the project team, communicate and manage their blockchain environment.  This would lead to a dramatic reduction to response times should an malicious/security incident occur.

Such disruptions could include:
+ Impersonation of Project Team Members
+ Flooding Communication Mediums
+ DoS Communication & Management Mediums
+ Revoke or Lockout Access/Certificates/Credentials

<a id="DDOS_ATTK_TX"></a>

### Transaction Throughput
Blockchain ecosystems tend to use Transactions Per Second (TPS) as a benchmark; this is due to most systems having a capacity/limit on how quickly blocks can be produced and how many transactions can fit inside a single block.

Think of this as a train station, a train will come along at regular intervals but can only hold soo many people.  What happens if there are more people than space?  Some have to wait for the next train, what happens if this process is repeated again, and again, and again?  

An example is here [^3] where the Solana chain, at the peak of attack, experienced 400,000 transactions.  Now that is going to give anyone a bad day!  The result, the block producer (validator) ran out of memory and stopped functioning.

There could be other consequences of these attacks, such as:

+ Ledger Becomes Bloated 
+ Logs Expand Dramatically (Filling Disk Space)
+ Network Congestion


<a id="DDOS_ATTK_Cons"></a>

### Consensus Delay
The consensus mechanism is one of if not the most important component of a blockchain ecosystem.  This mechanism enforces data integrity and aids in determining the security, scalability and speed of transactions on the network [^4].

Attackers could attempt to target the blockchain consensus in a number of differing ways, these would include:

<a id="DDOS_ATTK_Cons_fblock"></a>
**Injection of False/Incorrect Blocks**

It could be possible for an attacker to inject false blocks that may appear valid to the consensus, however the ultimate goal would be to fork the chain in order to perform attacks such as `Long Range` or `Double Spending`. **(## LINK TO MD's ##)**

<a id="DDOS_ATTK_Cons_blockdelay"></a>
**Delay or Increase The Introduction of Blocks**

An attacker could choose to delay or increase block production, in order to affect consensus settings such as mining difficulty.  In both scenarios, investigating, rejecting and re-organising blocks can be time consuming.  As such, this can be exploited by attackers to affect time-sensitive systems and/or game the system itself (e.g. increase mining difficulty so other miners move onto other projects)

<a id="DDOS_ATTK_Cons_voting"></a>
**Target Voting/Consensus Threshold**

Most blockchains implement a form of either a Craft Fault Tolerance (CFT) or Byzantine Fault Tolerance (BFT) consensus mechanism [^4].




[^1]: Bitcoin Developer Guide
  https://btcinformation.org/en/developer-guide#p2p-network
[^2]: Man in the middle (MITM) attack
  https://www.imperva.com/learn/application-security/man-in-the-middle-attack-mitm/
[^3]: Solana: 9-14 Network Outage Initial Overview
  https://solana.com/news/9-14-network-outage-initial-overview
[^4]: Impact of Consensus Protocol on Throughput
  https://www.nec.com/en/global/insights/article/2020022520/index.html
[^5]: What are Governance Tokens? How Token Owners Shape a DAO's Direction
  https://decrypt.co/resources/what-are-governance-tokens-how-token-owners-shape-dao
[^6]: Terra Blockchain Officially Halted to Prevent Governance Attack
  https://cryptopotato.com/terra-blockchain-officially-halted-to-prevent-governance-attack/