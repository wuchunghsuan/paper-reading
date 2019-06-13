# Tail Latency

## [EuroSys ’19] Managing Tail Latency in Datacenter-Scale File Systems Under Production Constraints

- Motivation
  - Large-scale distributed systems exhibit unpredictable high-percentile (tail) latency variations.
    - component failures, replication overhead, load imbalance, and resource contention.
- Resource-harvesting datacenters?
  - two isolation mechanisms to protect the co-located services
    - **throttling** of the data access throughput of the server (at 60MB/sec)
    - a “busy” flag that informs the corresponding metadata manager and clients that the server cannot take more access load.
- Goal:
  - Seek the best tail latency for the **batch workloads**
  - Do not concern the resource contention with other services.
- Job performance may vary 60× or more, due to tail data access latencies
- Main reasons of tail-latency:
  - long disk queues
  - server-side throttling
- CurtailHDFS
  - “fail fast” for writes
    - detects and replaces the slowest server in a pipeline.
  - “smart hedging” for reads
    - monitors the server’s performance on a per-packet basis, and starts a “hedge” (duplicate) request when performance starts to degrade.