Part 1; high level overview, process nodes get PC (mention oracle)

- introduction with problem definition

Part 2: support: blockchain and privacy solution: SN

Optional now: Attacks

Part 3: comapire papers



# Paper

<span style="color:red;">TODO</span>:

- I used bullet points a lot in the following paper to organize logic, but those will be combined into single lines in the future.

- As the latter sections of the paper become more detailed, the introduction may become outdated. Therefore, I will revisit and update the introduction with more accurate details at the end.

<span style="color:red;">Names</span>:

- DPoL:  Decentralized and infrastructure-independent Proof-of-Location
- BLIP: Blockchain-based Location Integrity and Provenance for Mobile Phones
- Leveraging Secret Network for a Decentralized and Infrastructure-Independent Proof-of-Location Scheme



## Introduction

##### Random Talk:

The increasing demand for location-based services (LBS) has prompted the development of more secure, reliable, and privacy-preserving methods for verifying the location integrity and provenance of mobile devices.

##### Problem:

<span style="color:red;">[Mention existing best approch (which is centrolized) implemention to make sure they know whats role Verifier and CA is playing]</span>

Traditional centralized verifier and Certificate Authority (CA) systems have inherent limitations, such as

1. dependence on trusted third parties, 
   - vulnerability to single points of failure, and potential privacy breaches. 
2. more

In recent years, blockchain technology has emerged as a promising alternative, offering a decentralized, <span style="color:red;">transparent</span>, and tamper-proof infrastructure for managing location data.

##### Solution:

In this paper, we propose a novel decentralized and infrastructure-independent proof-of-location (DPoL) scheme for mobile phones, leveraging the Secret Network blockchain and short-range communication technologies such as Bluetooth. 

- <span style="color:red;">We adapt their principles to the Secret Network blockchain, thereby eliminating the need for centralized verifiers and CAs. </span>
- Our approach builds upon existing research in 
  - APPLAUS: Toward Privacy Preserving and Collusion Resistance in a Location Proof Updating System by Zhu et al.
  - blockchain-based proof-of-location, such as the work by Amoretti et al.
  - CLIP: Continuous Location Integrity and Provenance for Mobile Phones by Lyu et al.
  - Practical implementations like 
    - Secret Network whitepaper
    - Helium whitepapers
    - FOAM whitepaper
    - A Study of Blockchain Oracles by Abdeljalil Beniiche
  - Furthermore, we consider the privacy aspects of commercial location-based services, taking into account Apple's Location Services Privacy Overview.

Our DPoL scheme employs the Secret Network's unique privacy-preserving smart contracts, called secret contracts, to store, process, and verify location proofs. These secret contracts enable secure, private, and auditable computations, which ensures user confidentiality while maintaining the transparency and security of a blockchain. By utilizing short-range communication technologies, our scheme allows mobile devices to establish secure connections with neighboring devices, exchange location proofs, and submit these proofs to the Secret Network for verification.

##### Layout:

The remainder of this paper is structured as follows: 

- Section II provides a comprehensive background on location-based services, centralized and decentralized approaches, and the Secret Network blockchain. 
- Section III presents the architecture and design of our proposed DPoL scheme, detailing the components, protocols, and algorithms involved. 
- Section IV evaluates the performance, security, and privacy aspects of our solution, comparing it to existing approaches. 
- Finally, Section V concludes the paper and discusses future research directions.



> <span style="color:red;">Other Aspect or Interesting fact: want to mention Oracle but maybe not in this paragraph</span>
>
> They act as Oracles and help solve **Oracle problems** (W1 paper)
>
> An interesting aspect of our proposed solution, when compared to existing approaches, can be seen in the context of an oracle that bridges the gap between off-chain data and on-chain processing. Traditional systems involve 
>
> - peer-to-peer Bluetooth nodes (<span style="color:red;">Web 2.0?</span>) communicating with a 
> - centralized verifier (Web 2.0) for location data validation. 
>
> In contrast, our approach maintains the 
>
> - peer-to-peer Bluetooth nodes (<span style="color:red;">Web 2.0?</span>) but connects them with the 
> - Secret Network (Web 3.0), effectively creating an oracle-like system that links real-world location data with the decentralized blockchain infrastructure. 



## The Location Proof System <span style="color:red;">or Prove of Location</span>

#### System Model: 

The system model includes the following types of parties involved:

- Users: Individuals act as nodes support short-range communication technology like bluetooth.
  - Prover requerst location proof
  - Witness helps generate proof
- Verifiers: Parties interested in verifying the location proof provided by users. These may include service providers, security agencies, or other users.
- <span style="color:red;">Model: Blockchain / Oracle, not keep mention Secret Network</span>: A decentralized network that facilitates secure and privacy-preserving transactions, storage, and verification of location proofs.

#### Location Uploading Structure:

>
> just intro the relation between parties, then mention different with Helium ...
> then add privacy using different way

##### Joining the Network: 

1. <span style="color:red;">Install the necessary software on the device. (I think we dont mention such details)</span>

2. Generate a unique identifier (public-private key pair) with the Blockchain <span style="color:red;">(start mention Secret Network in next section?)</span>. *using network connection*

3. Discover the network and its peers and the new node will start contributing to the Proof of Location now. *using bluetooth+network connection*

   Broadcast a *location proof request* to nearby nodes in the peer-to-peer Bluetooth mobile network.

   - Prover:
     - **Poisson distribution** as the rate at which location proofs are updated. By using this method, they can make it harder for people to figure out where you are by looking at the updates. 
     - **Periodically changed pseudonyms** are used by the mobile devices to protect source location privacy from each other, and from the untrusted location proof server.
   - Witness:
     - **User-centric location privacy model** in which individual users evaluate their location privacy levels and decide whether and when to accept the location proof requests.

   Tiers of approches (location proof request):

   1. Envelope of envelopes (Useful when checking stationary nodes)

      Since it does not involve blockchain calculations, the computation time is faster, making it worthwhile to explore this approach further. To make it work between non-stationary nodes, we could allow some layers of encryption to be decrypted by more than one node, depending on the signal strength (similar to a BFS tree where each directed edge represents a Bluetooth connection). 

      However, the issue is that the information obtained using this approach is the same as that in the next approach

   2. Uploading list of signed proof by both nodes

      For each nearby peer, send a signed location proof request. The peer will then sign this location proof request and upload it to the blockchain.

      However, the issue is that the information obtained using this approach is the same as that in the next approach.

   3. Uploading list of nearby public keys (Current Solution <span style="color:red;"> but I probobaly wrong since its different with other papers</span>)

      When discussing collusion attacks, one potential scenario involves sending location proof request requests through the network instead of using Bluetooth, In this case, false location proof request could still be signed & uploaded to the network. Therefore, the step of "signing" the location proof request might not provide significant security benefits on its own.

   Indeed, even when tiers 1 and 2 attempt to conduct some local verification before updating the location on the blockchain, they might not provide more information than tier 3. Consequently, the blockchain is required to determine which node is dishonest when validation takes place

##### Generation of Presence Claim: 

1. Presence claim request:
   - Prover public key, Verifier public key
   - Presence claim avaliable / expire time (when can verifier validate the Presence claim)
   - timestamp (where is prover yesterday)
   - granularity level
2. Private Smart Contract technology (e.g., Secret Network)
3. time-windowed presence claims & any granularity levels 

##### Verification of Presence Claim: 

1. Request the location proof from the Secret Network.

2. As we have defined a structure/scheme that collects user location data and a "decentralized" server to access the collected data and perform verification calculations, it is important to recognize that no distribution of speed and accuracy of verification calculations can satisfy all practical applications, particularly in the B2B domain. Fortunately, the scheme we have defined can directly utilize existing applications from centralized location proof systems or graph theory. 

   > For example, 
   >
   > some business can implement machine learning on the blockchain to decentralize the process of distinguishing cheating nodes within the network. 
   >
   > some can trust any location proof hence always generates presence claim if its meets their requirement
   >
   > some could just pick random node and consider it as cheating.

   In this paper, we will introduce an example of how to enable smart contracts to efficiently identify dishonest nodes on the network, incorporating elements of reputation systems that pervents colluding attacks.

   ##### Example:

   Paper13: **betweenness ranking-based** and correlation **clustering-based** approaches for outlier detection





> By combining the principles of APPLAUS, blockchain-based proof-of-location, and Secret Network, this decentralized infrastructure-independent proof-of-location scheme leverages a peer-to-peer Bluetooth mobile network to provide a secure, privacy-preserving, and efficient method for verifying location data without relying on fixed nodes. This scheme has applications in a variety of fields, including supply chain management, location-based services, and security applications.



## Other Works

Traditional PoL systems often rely on centralized verifiers or certificate authorities (CAs), which present a single point of failure and vulnerability to collusion attacks. To address these issues, there is a growing interest in leveraging blockchain technology to design decentralized PoL systems. Among different blockchain platforms, the Secret Network has emerged as a promising solution to provide privacy-preserving and collusion-resistant PoL systems.

##### Tiers of methods for location proof:

1. Normal LBS: Users upload their GPS location to a centralized server, but this approach cannot prevent hacks like those in Pokémon Go.

2. Traditional PoL: Relies on centralized verifiers and Certificate Authorities (CAs).

3. Existing Blockchain-based Proof of Location: Addresses some issues but still has privacy concerns related to user identity.

4. Blockchain + <span style="color:red;">Private Smart Contract technology (e.g., Secret Network)</span>: 

   > (privaty perserving blockchain)
   > Missing Peer to Peer part:
   >
   > - Make it sounds more like my approch sloves problem not just mention Secret Network

   - Resolves the issues mentioned above (centralized&privacy) (almost all papers)
   - Supports history location proof
   - Supports time-windowed presence claims. (paper 02, whitepaper 04/07)
   - Supports any granularity levels instead of harded coded integer number of levels and gereate 5 proofs when there is 5 granularity levels (paper05)

In summary, the four tiers of location proof methods progress from normal location-based services with centralized servers, through traditional PoL systems with centralized verifiers and CAs, to existing blockchain-based PoL solutions with lingering privacy issues. Finally, blockchain combined with private smart contract technology, such as Secret Network, provides a comprehensive solution that addresses privacy, security, and time-windowed presence claims.



## Other Topics

#### Test Cases:

1. Wormhole attack
   - Short-range communication technology hardware is capable of doing long-range.
2. Sybil attacks and Collusion attacks
3. Replay attack
4. Cheating on own geographic location

#### Privacy:

> The classic blockchain trilemma (Security/Decentralization/Speed) is insufficient when describing the web3 applications. I define the application tetralemma (Security/Decentralization/Speed+Privacy), which is more suitable to most recent web3 projects like Secret Network.

Nodes have complete control over the time and target they want to expose their Presence Claim. Secret Network powers this flexibility and privacy.





> Next week:
>
> 1. Mention Privaty Perserving Blockchain (Oracle) instead of Sercet Network
> 2. Add future work section for the topics like Envelope
> 3. New Strucure:
>    1. Introduction: the PoL model is same as this one but then we will do privacy
>    2. Approach:
>       - Section1: 
>         - just describe about model, describe we similar but fine
>         - but it looks like the way we process PC are different -> maybe we could also be diff
>           - do they sloving problem that only happen in centrolized structure (verifier and node?)
>           - we similar or we diff, is it better or worse?
>       - Section2: **privacy** part: 
>         - they have centrol service we dont want that -> blockchain
>         - now we have privacy problem -> fix privacy problem
>         - then talk secret network in part2
> 4. Have two sections:
>    - peer to peer section 
>
> 





## 08_CLIP_Continuous_Location_Integrity_and_Provenance_for_Mobile_Phones(Cited15)

> CLIP aims at providing the integrity of users’ mobility traces.
>
> Each node record all history sensor data (like signal strength for stationary user/witnesses)
>
> Sounds like Paper_02 Blockchain-based Proof of Location (Peer to Peer)
> Referenced as an infrastructure-independent approach by paper02 Blockchain-based Proof of Location.

<img src="/Users/soso/Desktop/Research/w8&9/Note8.assets/image-20230309185405374.png" alt="image-20230309185405374" style="zoom:150%;" />

##### Summary:

1. User(Prover) want to prove their location -> send request to Verifier
   - by internet

2. Verifier then contacts nearby Witness (AP or Peers) (distributed architecture)

   - Witnesses create SLPs based on their own sensor data and send to Verifier
     - SLP includes info about Witness's location and time

3. The Verifier collects all of the SLPs from nearby Witnesses and 

   - use SLPs to verify the Prover's presence at specific location points. 

     - checks each SLP matches up with mobility trace
     - involves comparing the information in each SLP with other sensor data collected by Wireless Access Points (APs) and other sources

     - "leverages existing resources, such as public road maps, available wireless APs or co-located mobile devices, for continuous location veriﬁcation."

   - checks with CA to check all parties involved are authorized and have valid digital certificates using Internet.

4. Return results to Prover (Presence Claim)

##### Request

Verifier (such as a government agency or a private company, that has the authority to verify the user's location) receive and check if mobility trace and SLPs of User (prover) are match up.

- mobility trace
  - generated by sensors already built into smartphones, like GPS, accelerometer, and magnetometer
  - sequence of past location points at corresponding time points
  - stored on the user's smartphone
  - send to verifier
- SLPs: Secure Location Proof (special codes)
  - witness generates the SLPs based on the user's location at a certain time
    - witness is a nearby mobile user or stationary wireless access point (AP) that agrees to create a Secure Location Proof (SLP) when they receive the prover's request.
  - stored by the user on their smartphone
  - send to verifier

##### Return

Prover receives the verification message contains a digital signature that is generated by the verifier's private key, which can be verified using the verifier's public key

## 13_Toward Privacy Preserving and Collusion Resistance in a Location Proof Updating System(Cited126)

>Cited by 02,08,12 mentioned APPLAUS
>
>APPLAUS: A Privacy-Preserving LocAtion proof Updating System
>
>- Bluetooth devices mutually generate location proofs and send updates to a location proof server.

Key Points

- **Periodically changed pseudonyms** are used by the mobile devices to protect source location privacy from each other, and from the untrusted location proof server.
  - Public key + Random String for every request (Pervent relay attacks)
- **User-centric location privacy model** in which individual users evaluate their location privacy levels and decide whether and when to accept the location proof requests.
  - High Privacy -> Ask less witnesses nearby
    - Based on this evaluation, the requesting device decides whether or not to accept a location proof exchange request from another device.

- Against Colluding Attacks
  - Approaches for outlier detection
    - Betweenness ranking-based:
      - Importance: the algorithm looks at how many times that pseudonym appears on the shortest path between any two other pseudonyms in the graph
      - Then rank all of the pseudonyms based on their importance value
      - Low importance ranking node is suspicious nodes
    - Correlation clustering-based:
      - Make a temporal-weighted graph which grouping similar location proofs together based on their time delay, if two proofs are received within a short time frame of each other, they might be grouped together because they are likely to be from the same user.
      - Once all of the similar location proofs have been grouped together, suspicious location proofs are identified as those that do not fit well into any of these groups
  - **Poisson distribution**
    - In this scheme, the prover periodically sends out a location proof request to its neighboring devices through Bluetooth.
    - Authors chose to use Poisson distribution as a way to control the rate at which location proofs are updated. By using this method, they can make it harder for people to figure out where you are by looking at the updates. 

When a new node (such as a person's phone or other device) wants to join the network, it must go through the following steps: 

1. Generate a set of M public/private key pairs: The new node generates a set of M public/private key pairs, where M is a predetermined number. 
2. Register with the Certificate Authority (CA): The new node registers with the online CA by sending its public keys to the CA. The CA then associates these public keys with the real identity of the new node in its database.
3. Preload public/private key pairs: The new node preloads its set of M public/private key pairs before entering the network.
4. Broadcast location proof requests: When the new node needs to collect location proofs from its neighboring nodes, it broadcasts a location proof request through Bluetooth.
5. Once a neighboring node agrees to provide location proof for the new node, this node becomes a witness of the new node. The witness generates a location proof and sends it back to the new node.
6. Verify location proofs: The server verifies that the location proofs provided by witnesses are consistent with each other and that they match up with what is expected based on other information collected from nearby nodes.
7. Overall, these steps allow for secure and private joining of mobile nodes into the network while also enabling them to collect and verify location proofs when necessary.



# Paper

### Problem Definition

##### Want to Slove: 

> Decentralized and infrastructure-independent proof-of-location scheme using short-range communication technologies such as Bluetooth

##### Problem Analysis:

> The different PoL schemes may have a different flow, but generally, we could break them into several parts:

1. New Node joins the network

2. Generates a "Presence Claim."

   - A node sends a request.

   - Other nodes generate.

3. Verify the Presence Claim


##### Presence Claim vs PoL:



##### Available Tools:

1. Prove of Coverage
   - Inspired by the Guided Tour Protocol 
   - **envelope** of envelopes: Use **network connection** to help validate Bluetooth connection.

2. Secret Network:

   - We dont need granularity level from paper05, paper08

3. Connection:

   > Paper02: We consider an LBS-oriented peer-to-peer network with mobile nodes that are connected to the Internet through the WiFi or cellular network interface, and are able to exchange information with neighboring nodes through short-range communication technologies such as Bluetooth

   - Combination of Short-range Communication Technologies
     - Bluetooth/Wifi/NFC/QR code
   - Long-range Communication that communicates with blockchain.

##### Magic Variables to Solve the Problem:

- **Infrastructure-independent** vs Infrastructure-dependent

- Allow disconnected graph

- Aggregation/reputation system?

- The minimum number of nodes involved when generating a presence claim

  - Small

    - the schema will have low security
    - At least 2 to communicate with the network (user & node)

  - Large

    - the schema will have low scalability, giving the network a higher chance of not being available.

  - Dynamic

    > How to get large numbers while keeping scalability

    - Contracting multiple stages for the project using decentralized governance(improvement proposal) or a hardcoded timer:

    - FOAM's example (paper04):

      > FOAM using the infrastructure-dependent approach, a set of Zone Anchors are assumed to be available to produce proofs of the location to users.

      Stage 1: provides Token Curated Registries(TCR), which record the Points of Interest(POI) the community maintains. When the number of POI reaches a number, the project enters stage

      > They designed a native protocol token that incentivizes the marketplace between consumers(want to utilize the list), candidates(want to be on the list), and token holders.
      >
      > Notice we are not a project whitepaper. This part shows how protocol design could push the project through the stage. 
      
      Stage 2: The TCR accumulates enough information in a decentralized manner, so the FOAM can provide PoL services with a high minimum number of nodes involved (1 user + 4 anchors) when generating a presence claim.

- The number of roles that can be played

  - User + subset of {Prover, Verifiers, Anchor, Authority, ....}

- Retroactive vs Proactive location proof (paper05)

  - A retroactive location proof: collect location proofs when aksed (user check-in at the conference)
    - (PoL with SN) (support "around" using PC history)

  - A proactive location proof: collect location proofs continuously (notify user conference nearby)
    - (PC)



### Proposed Configurations

#### Configuration 0:

> Decision that seems reasonable for now

##### Properties:

1. Infrastructure-independent
2. Not allow disconnected graph (allow PC but PoL limited)
3. Aggregation/reputation system: need
   - option1: compute during PoL
   - option2: node have a reputation
4. Communication:
   - Short-range with neighbors:
     - Communicate with all reachable nodes to get as much data as possible for the network.
   - Long-range with blockchain: 
     - accept or request tasks that implicitly cause role change for some "random" node on the network.
5. Minimum number of neighbors: 1 
   - maybe Min number of Betweenness more useful
6. States of a Node:
   - User/Witness PC=(User,Witness)
   - Challenger (Envelope of Envelopes or Multi-Layer Data Packet)
     - requesting PoL
     - Could be Application vs Random node
   - Target (Envelope of Envelopes)
   - ~~Verifier/Application/Router~~ (not a node)
7. Proactive location proof: collect PC continuously

#### Configuration 2:

> This configuration focuses on **proactive location proof**. 
>
> The network takes regular snapshots of every 'neighbor pair,' which are added to the list S along with the time they were taken. 
>
> Network nodes are also occupied with processing the oldest snapshots in S. This processing involves removing/adding the 'neighbor pair' using all available information (utilizing game theory/machine learning/Pokemon Go's cheating detection).
>
> The processing method could be improved by adding a improvement proposal.
>
> New users are required to participate in several snapshots before being able to provide a usable PoL in the archived snapshots.
>
> The PoL only contains information about the user's trajectory, which may not be suitable for most real-time games.

This configuration supports an aggregation/reputation system, which means that the PoL approach can utilize all the information available in the network (depending on the processing method). Logically, this makes it the most secure PoL approach.

Replace snapshot with PC

Paper mention few possible processing method.



#### Test Cases:

1. Wormhole attack
   - Short-range communication technology hardware is capable of doing long-range.
2. Sybil attacks and Collusion attacks
3. Replay attack
4. Cheating on own geographic location



#### Privacy:

> The classic blockchain trilemma (Security/Decentralization/Speed) is insufficient when describing the web3 applications. I define the application tetralemma (Security/Decentralization/Speed+Privacy), which is more suitable to most recent web3 projects like Secret Network.

Nodes have complete control over the time and target they want to expose their Presence Claim. Secret Network powers this flexibility and privacy.



