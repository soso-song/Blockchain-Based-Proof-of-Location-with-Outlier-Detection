# W7 Target:

1. Check more Peer to Peer paper
1. Chek Guided Tour Protocol & relation with paper02
1. Recall how past papers (i.e., 02, 05, 07) helped on my paper and copy the selected information/paragraphs to generate an example paper.



## How does paper 00~07 Related to PoL Problem

### 02



### 05



### 07



## Example Paper generated from the Information I have

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

      Stage 1: provides Token Curated Registries(TCR), which record the Points of Interest(POI) the community maintains. When the number of POI reaches a number, the project enters stage 2.

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



#### Configuration 1 (Failed):

> This configuration aims to find an instance of why "**Envelope of Envelopes**" is helpful in our infrastructure-independent Bluetooth network.
>
> Envelope of Envelopes is a way to check whether a path/chain exists between nodes using Bluetooth. It detects false/outdated "neighbor tuples" in the network memory.
> It is designed to check the connectivity of Anchors\APs that are **not moving** in an **infrastructure dependents** approach. 
>
> Hence there are limited ways to apply "envelope in envelopes" in an infrastructure-independent scheme where every node dynamically changes its location.
>
> Claim:
>
> 1. Only connected graphs can prevent Sybil/Collusion attacks.
> 2. The 'envelope operation' should only be performed when generating location proof.
>
> The primary goal of the 'envelope operation' is to verify that the subgraph containing the user and witness is connected to the remainder of the graph: user/witness<->network
>
> The challenger, which is a random node, generates a list of targets T that includes the user, witness nodes, and their neighbors (i.e., the edges of the network). 
>
> However, this list T is determined by the spanning tree that was generated beforehand, which doesn't offer randomness against potential attacks.

The node that generates the proof is not necessarily the user's neighbor. If we choose multiple nodes that are implicitly connected to the user, the path of the envelope will always pass through the first two levels of the spanning tree. As a result, we cannot detect whether a wormhole attack has occurred at level 1 of the tree (i.e., the user's neighbor).



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



#### Configuration 3:

> **Infrastructure-dependent**: Let's bring back Ancher/AP and create something similar to Helium using the Secret Network
>
> This can significantly increase the number of trilateration in the system, as every node has a higher chance of being covered by multiple high-reputation antennae in the network. This makes the system more resilient against attacks, increasing its attack resistance from just 1% to almost 50% locally.

##### Properties:

None

##### Generation of Location Proof:

None

##### Verification of Location Proof:

None



#### Test Cases:

1. Wormhole attack
   - Short-range communication technology hardware is capable of doing long-range.
2. Sybil attacks and Collusion attacks
3. Replay attack
4. Cheating on own geographic location



#### Privacy:

> The classic blockchain trilemma (Security/Decentralization/Speed) is insufficient when describing the web3 applications. I define the application tetralemma (Security/Decentralization/Speed+Privacy), which is more suitable to most recent web3 projects like Secret Network.

Nodes have complete control over the time and target they want to expose their Presence Claim. Secret Network powers this flexibility and privacy.
