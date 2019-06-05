# Co-flow

## The Coﬂow Abstraction

- Coflow = **a collection of flows that share a common performance goal**,
e.g., minimizing the completion time of the latest ﬂow or ensuring that flows meet a common deadline.

- **Shuffle** in MapReduce is also one of examples of coflows.

- Instead of improving network-level metrics that can be at odds with application-level goals, coflows improve performance through application-aware management of network resources.

## **[SIGCOMM '11] Managing data transfers in computer clusters with orchestra**

- Motivation Examples
  - Facebook, Twitter, Netflix
- **Orchestra** - a global control architecture to manage intra- and inter-transfer activities.
  - Focus on two transfer pattern: *shuffle* and *broadcast*
  - users’ applications (i.e., MapReduce jobs) need not change
- Implementation
  - Inter-Transfer Scheduling
    - **Weighted fair sharing**: each transfer is assigned a weight, and each congested link in the network is shared proportionally to the weights of the transfers using that link.
    - Orchestra use this mechanism to emulate scheduling policies (e.g. fair sharing, FIFO and priority) without changes to routers and switches.
    - Allowing different transfers to use different numbers of TCP connections per host.
  - Broadcast Transfers
    - centralized storage system can be bottleneck
    - **Cornet** - BitTorrent-like protocol optimized for datacenters
      - Use large blocks
      - No leechers
      - use simple integrity check
  - Shuffle Transfers
    - A simple optimality criterion: **fully utilized link**
      - *an optimal shuffle schedule keeps at least one link fully utilized throughout the transfer.*
    - Analyze the performance of using different connection number of receivers in Section 6.2.
    - Unweighted fair sharing can show poor performance in data skew
    - Weighted Shuffle Scheduling (WSS) Algorithm:
      - allocate rates to each ﬂow using weighted fair sharing
      - Improve shuffle speeds by 29%

## [Hotnets ’12]Coflow: A Networking Abstraction for Cluster Applications

- coflow - a networking abstraction to express the communication requirements of prevalent data parallel programming paradigms.

## **[SIGCOMM’ 14]** Efficient Coflow Scheduling with Varys

- Study the inter-coﬂow scheduling problem for arbitrary coﬂows and focus on two objectives:
    1. improving application-level performance by minimizing CCTs
    2. and guaranteeing predictable completions within coﬂow deadlines
- The two objectives above is **NP-hard**.
  - They reduce *concurrent open shop scheduling problem* to coﬂow scheduling problem.
  - Concurrent open shop scheduling problem - <https://link.springer.com/article/10.1007%2Fs10951-006-7042-y>
- Coflow scheduler's goals:
    1. *Stavation freedom*
    2. *Work-conserving allocation*
    3. *Guaranteed completion*
- Other solutions:
  - Shortest-process-time-first(SPTF):
- ***Varys*** - provides a simple API that allows data parallel frameworks to express their communication requirements as coflows with minimal changes to the framework.
  - *Smallest-Effective-Bottleneck-First (SEBF)* heuristic
    - greedily schedules a coflow based on its bottleneck’s completion time.
  - *Minimum-Allocation-for-Desired-Duration (MADD)* algorithm
    - allocate rates to its individual flows
- Evaluation
  - 100-machine EC2 cluster
  - replaying production traces from Facebook

## [SIGCOMM ’15] Efficient coflow scheduling without prior knowledge

- ***Coﬂow-Aware Least-Attained Service (CLAS)*** – to minimize the average CCT without any prior knowledge of coﬂow characteristics
- Aalo - a system that supports coﬂow dependencies and pipelines, and works well in presence of cluster dynamics like multi-wave scheduling.
  - requires **no prior knowledge** of coﬂow characteristics, e.g., coﬂow size, number of flows in the coﬂow, or its endpoints.
  - without any changes to the network or user jobs.

## [SIGCOMM '18] Sincronia: near-optimal network design for coflows

- A practical near-optimal network design for coflows still remains elusive. Two reasons:
  1. requires knowledge about location of congestion and paths taken by each (co)flow, making it hard to implement in the fabric core and/or changes dynamically.
  2. Since rates allocated to flows are correlated, reallocation is impractical in datacenters where thousands of coflows may arrive each second.
- Sincronia -  near-optimal network design for coflows