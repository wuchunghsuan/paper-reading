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

## [Mass Storage Systems and Technologies '19] BFO: Batch-File Operations on Massive Files for Consistent Performance Improvement

- Existing file systems only provide single-file access pattern.
- This paper focuses on optimizing the file operations when processing a large number of files.
- Existing solutions:
  - Muti-thresding
  - Prefetching: data locality
  - solid-state
- BFO: a novel Batch-File access mechanism
- Key idea:
  - Treat metadata differently from file data, and process each type in a batch separately from the other, and further re-order and optimize the storage I/Os when accessing a batch of files.
- Batch-File Read (BFOr):
  - Two phases:
    - scans the metadata of all directories and files to determine their data locations
    - then leverages a layout-aware I/O scheduling policy to read these data with a minimal number of large I/Os
  - Layout-aware Scheduling: sort and merge the data segments
- Batch-File Write (BFOw):
  - Two phases:
    - first stores all file data of multiple files into contiguous free blocks,
    - and then updates their corresponding file metadata to be eventually flushed to disks with the fewest large I/O operations
- **Portability**: without modifying the latters data structures and existing procedures.
- Problem Analysis:
  - Random read 4KB-sized files:
    - HDD: 57.8x longer than sequential read.
    - SSD: 2.6x
  - BFO Improvement:
    - Random read 4KB-sized files:
      - RAID: 42.1x
      - HDD: 22.4x
      - SSD: 81.4%
    - Sequential Read: 1.6×, 2.0×, and 1.8×
    - Random write: 71.8×, 111.4× and 2.9×