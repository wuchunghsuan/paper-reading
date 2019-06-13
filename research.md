# Research

### [IEEE Transactions on Information Theory '2019] Coded Computation over Heterogeneous Clusters

- **Coding & Heterogeneous**: Propose a coding framework for speeding up distributed computing in heterogeneous clusters by trading redundancy for reducing the latency of computation.
- Recent usage for coding:
  - Deal with the **communication**
  - and **straggler bottlenecks**
- Summarize recent paper about coding.

### [IEEE International Symposium on Information Theory '2017] A pliable index coding approach to data shuffling

- use index coding to improve the shuffle

### [IEEE International Symposium on Information Theory '2018] A Fundamental Tradeoff Between Computation and Communication in Distributed Computing

- Coded distributed computing(CDC)
  - reduce the load of data shufﬂing via coding
- Use redundancy in map computation to reduce the communication load.

### [International Parallel and Distributed Processing Symposium '2015] Resource and Deadline-aware Job Scheduling in Dynamic Hadoop Clusters

- Predict the job completion time in a *dynamic* Hadoop
environment.
- Minimizing job deadline misses.
- Use a self-learning model to estimate job completion times and use a model to predict future resource availability.
  
### [IEEE International Conference on Cloud Computing '2014] FRESH: Fair and Efficient Slot Configuration and Scheduling for Hadoop Clusters

- Slot configuration is important but static and fiexed.
- FRESH provide best slot setting, dynamically configure slots, and appropriately assign tasks to the available slots.

### [TPDS '2017] Moving Hadoop into the Cloud with Flexible Slot Management and Speculative Execution

- **Stragglers**: automatically identifies map stragglers and resizes their slots accordingly to accelerate task execution.
- **Data skew**: mitigate data skew with an adaptive speculative execution strategy.
- **Configuration**: Adaptively changes the number of slots to balance the resource usage.

### [Journal of Grid Computing '2015] Improving MapReduce Performance with Partial Speculative Execution

- **Speculative Execution**: propose the Partial Speculative Execution (PSE) strategy to make speculative tasks start from the checkpoint.
- Eliminate the costs of re-reading, re-copying, and re-computing the processed data