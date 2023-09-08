## This week update:

New Paper:

- 20_Attack Robustness and Centrality of Complex Networks

TODO:

- Find outlier detection method in a P2P (peer-to-peer) network for preventing colluding attacks

  - 17_Outlier Detection in Network Data using the Betweenness centrality

  - 19_Collusion in peer-to-peer systems

  - 18_Blockchain Based Zero-Knowledge Proof of Location in IoT

- Efficiency Simulation



## Summary:

I read this 20_Attack Robustness and Centrality of Complex Networks and roughly summed up the big picture and the next steps: 

- goal: outlier detection methods in a P2P (peer-to-peer) network for preventing colluding attacks.

- I should find a method from other papers, current method:
  - Betweenness Ranking
    - Need more time reading:
      - 17_Outlier Detection in Network Data using the Betweenness centrality
      - 20_Attack Robustness and Centrality of Complex Networks
  - Correlation Clustering
    - 13_Toward Privacy Preserving and Collusion Resistance in a Location Proof Updating System
      - 16_Correlation clustering in general weighted graphs
  - More Method?:
    - 19_Collusion_in_P2P_systems(Cited 50)
    - 09_Ghost_Riders_Sybil_Attacks_on_Crowdsourced_Mobile_Mapping_Services(Cited40)
    - 18_Blockchain_Based_Zero-Knowledge_Proof_of_Location_in_IoT(Cited 16)
    - 11_Robust_Decentralized_PoL(Cited3)
    - 12_Incentive_Mechanism(Cited3)
- If I'm unlucky, I might have to invent a method myself, which would make my paper longer. However, I'll try to read more to prevent this from happening.



## 20_Attack Robustness and Centrality of Complex Networks

##### Model Networks with Simultaneous Targeted Attacks

> Simultaneous targeted attacks: Attacking the network by removing multiple vertices at once.
>
> Model networks: Theoretical or simulated networks used for studying network properties and behaviors, as opposed to empirical networks.
>
> **Degree centrality**: The number of connections a vertex has to other vertices in the network.

For simultaneous targeted attacks on most model networks, removing vertices in decreasing order of degree is the most effective way to degrade the network.

##### All Networks with Sequential Targeted Attacks

> Sequential targeted attacks: Attacking the network by removing vertices one after another in a specific order.
>
> **Betweenness centrality**: A measure of how important a vertex is in connecting different parts of the network.
>
> **Closeness centrality**: A measure of how close a vertex is to all other vertices in the network, indicating how quickly information can spread from that vertex to others.
>
> **Eigenvector centrality**: A measure of a vertex's influence in the network, considering not only its connections but also the importance of the vertices it is connected to.

For sequential targeted attacks on all networks considered, removing vertices based on betweenness centrality is the most effective way to degrade network structure.

Closeness centrality is almost as effective as betweenness centrality for sequential targeted attacks on networks.

Eigenvector and degree centrality are the least effective methods for exposing network vulnerability under sequential targeted attacks.

##### Assortative Networks

> Assortative networks: Networks in which vertices with similar degrees tend to connect with each other.

For assortative networks, initially, removing vertices based on betweenness centrality is more effective, but eventually, degree-based removal becomes more effective again.

##### Empirical networks vs Model networks

> Empirical networks: Real-world networks based on observed data, as opposed to model networks, which are theoretical or simulated networks.

There are significant differences in the effectiveness of sequential targeted attacks based on different centrality measures for empirical networks compared to model networks.

Structural differences between model and empirical networks

> Structural differences between model and empirical networks: Differences in the way vertices and edges are arranged and connected in the network, affecting its properties and vulnerability to targeted attacks.

- The differences in vulnerability between model and empirical networks are due to subtle structural properties present in empirical networks but absent in model networks.
- The authors suggest that elucidating the nature of these structural differences is an interesting and important avenue for future research.

##### How does this paper relate to my interest:

> I am interested in outlier detection in a P2P (peer-to-peer) network for preventing colluding attacks.
>
> Currently, my focus is researching how betweenness is related to my topic.

1. This paper introduces other "siblings" of betweenness to me: Degree, Closeness, and Eigenvector centrality. This gives me a better understanding of the role betweenness centrality plays when discussing colluding attacks. If not, at least I've learned more "parameters" to consider when developing a better outlier detection method.
2. This paper introduces different types of networks (graphs), including "Empirical networks," which my interest lies in.
3. This paper emphasizes the significant differences that structural differences between model and empirical networks can cause, which is worth noting.
