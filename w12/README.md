## This week update:

This was a busy week; this PDF contains all my updates.

If you prefer text-based meetings or would like to change the frequency to once every two weeks, please feel free to do so. 

## Summary:

I conducted some research on Betweenness Ranking (Centrality):

1. Attempting to **convert ranking to a percentage** to evaluate the validity of PoL.
2. Finding the **best efficiency of this algorithm**, O(n^2), and discussing approaches to make it log time.

After this, I feel that Betweenness Centrality may serve as an auxiliary to the Connectivity-based approach. So, here is the structure:

I think the Clustering-based approach is better than the Connectivity-based approach, but both approaches seem to create a brand new topic, which is not included in the first 15 papers I have read (they all focus on PoL). That's why I added a few papers for me to read during the next week, which will mainly relate to algorithms about colluding attacks and outlier detection in P2P networks.

Papers:

- 20_Attack Robustness and Centrality of Complex Networks
- 17_Outlier Detection in Network Data using the Betweenness centrality
- 19_Collusion in peer-to-peer systems
- 18_Blockchain Based Zero-Knowledge Proof of Location in IoT



## Implementation(Outlier Detection):

#### Approach1: Connectivity-based:

Betweenness centrality (Betweenness ranking):

- Definition: a way of detecting the amount of influence a node has over the flow of information in a graph.
- Definition: a measure used in network analysis to identify the importance of individual nodes (or vertices) within a network.
- Meaning: Nodes with high betweenness centrality have a higher likelihood of occurring on a large number of shortest paths, indicating their significance in maintaining the overall connectivity of the network.

- Calculation: take every pair of the network and count how many times a node can interrupt the shortest paths (geodesic distance) between the two nodes of the pair.
  - <span style="color:orange;">Note: The geodesic distance depends on the **shortest path** over existing edges, while the Euclidean distance depends on the **straight-line** distance.</span>

**Convert Int to %**:

- [Paper15: APPLAUS]

  - It is often normalized by **dividing by the maximum possible number** of shortest paths that could pass through any node in the network, which depends on the network's size and structure.
  - Did not provide details about the attacks.

- [Paper02: Blockchain-based Proof of Location]

  - Referenced APPLAUS's betweenness approch

  - But they do talked about ROBUSTNESS ANALYSIS -> Colluding with other peers

    - didnt talk about betweenness ranking, mainly focus on using limitation of bluetooth range P2P verification to pervent Colluding attacks

    - When they talk about "letting the blockchain compute", there is a suspicion that all peers should calculate the betweenness ranking (mobile phone mining will consume a lot of resources)

      > Here is one example this paper doesn't makes sense:
      >
      > Two peers collude to build a false proof of location for one of them. The proof **may be** received by a honest peer that is far from the considered location and cannot contact the colluding nodes with the short-range communication technology. In this case, the honest peer may either immediately discard the proof of location (conservative approach) or make a more contemplated decision, **by evaluating** the betweenness of the two suspect peers, according to the procedure illustrated in Subsection 3.2.

    - <span style="color:red;"> I have multiple problems with this paper, I'll switch to other papers </span>

- [Paper17: Outlier Detection in Network Data using the Betweenness centrality]

  - given Betweenness Ranking(Centrality), find the outliers based on **p-value method**
    - To compute the p-value, we would need to perform a **statistical test** on the betweenness centrality values of the nodes, like
      - t-test
      - chi-squared test
      - this paper: "hypothesis testing"
    - <span style="color:red;"> Soso need more time to understand how this statistical stuff because they didn't define "Outlier"</span>
  - experiment: p-value was taken as 0.05. i.e., these experimental results have 95% confidence.
    - note: 95% = 1-0.05 such that if the p-value for a data point is less than or equal to 0.05, it is considered an outlier with a 95% confidence level.
  - Did not provide details about the attacks, didn't define outlier.

**Computationally Expensive**:

- O(mn^3) for unweighted graphs

- O(mn) time, O(n^2) space if using breadth-first search

- **Paper17**: O(n^2) time + O(n^2) for p-value method to compare each data point with other data points

- **Paper15 APPLAUS:** 

  - B(v) = $\sum_{s\neq v \neq t} \frac{\sigma_{st}(v)}{\sigma_{st}}$

  - Improvement 1:

    - The closer vertices can be computed from the dependencies of the farther vertices

    - Combine with **Paper15**: O(mn) time, O(n+m) space, which is still slow:

      ![image-20230406133736923](/Users/soso/Desktop/Research/FinalPaper.assets/image-20230406133736923.png)

  - Improvement 2:

    - Considering all the concurrent (within **60 seconds delay**) location proofs in a **region**, we first describe how to construct a pseudonym-correlation graph.

- Other Trade-Offs (Better than Improvement 2):

  > Instead of setting hardcoded ranges for temporal and spatial regions, there are better approaches to make the algorithm run in logarithmic time while the result reflects more accurate betweenness values across the entire network.
  >
  > Take note of the following methods that create a betweenness ranking for the entire network at any time (granularity may depend on the initial request). Once calculated, these ranking can be resued/shared for different location queries.
  >
  > This is somewhat similar to B2B. Depending on the user's purpose, 
  >
  > - they could use approximation, which fast and will improves over time. 
  >
  > - Alternatively, they could calculate the requested region and then, when not busy, connect all regions.
  
  - Approximation algorithms: Instead of calculating betweenness centrality for all pairs of nodes, approximation algorithms compute the betweenness centrality using a random sample of node pairs or a fixed number of randomly chosen nodes as sources. This reduces the computational complexity and can provide reasonably accurate estimates of betweenness centrality in many cases. One popular approximation algorithm is the Brandes' algorithm, which has a time complexity of O(nm), where n is the number of nodes and m is the number of edges.
  - Parallel and distributed computing: Another way to address the efficiency issue is by leveraging parallel and distributed computing resources. By dividing the task of computing betweenness centrality among multiple processors or machines, the overall computation time can be significantly reduced.
  - Incremental and decremental algorithms: In dynamic networks where nodes and edges are frequently added or removed, incremental and decremental algorithms can be used to update betweenness centrality values efficiently without recalculating them from scratch.
  - Using heuristics: In some cases, it might be possible to apply heuristics or domain-specific knowledge to reduce the search space and focus on the most important nodes, thereby reducing the computational complexity.

#### Approach2: Clustering-based (Correlation clustering):

> this is better approch, and I will attach it's image from past weeks
