# Research

## Hadoop Optimization

1. iShuffle - TPDS 2017
    - Flexible Reduce Dispatching
    - Preemptive Reduce Scheduling
    - Single-user
      - modify the Hadoop default scheduler (FIFO)
    - Multi-user
      - modify the Hadoop Fair Scheduler (HFS)
    - Experiments
      - **Simulate the other three different approaches**
      - Hibench
      - PUMA: Purdue mapreduce benchmark suite
      <https://engineering.purdue.edu/~puma/pumabenchmarks.htm>
      - SWIM: Statistical Workload Injection for MapReduce
      <https://github.com/SWIMProjectUCB/SWIM/wiki>
      - Workload: From Facebook, Cloudera

         CHEN, Yanpei; ALSPAUGH, Sara; KATZ, Randy. **_Interactive analytical processing in big data systems: A cross-industry study of mapreduce workloads._** Proceedings of the VLDB Endowment, 2012, 5.12: 1802-181

2. Hadoop-A - SC 2011
    - Use RDMA
    - A priority queue-based merge sort algorithm
    - Specific experiments
      - slow processors and memory buses
      - one round reduce
    - Deficiencies:
      - the building of the priority queue poses extra delay
      - the remote disk access in an Ethernet environment is signiﬁcant slower than that ondisk access
3. Sailfish - SOCC 2012 - Microsoft
    - It proposed I-File, a data aggregation system for intermediate data
    - Repartitions the intermediate data and dynamically determined the number of reduce tasks
    - Experiments
      - **Based on cluster workloads at Yahoo!:**

        A small fraction of the daily workload (about 5% of the jobs) use well over 90% of the cluster’s resources. These jobs
        1. Involve thousands of tasks
        2. Run for several hours
        3. Generate intermediate data that is at least as big as the input
      - Classifying MapReduce jobs in 6 general types
        1. Skew in map output
        2. Skew in reduce input
        3. Incremental computation
        4. Big data
        5. Data explosion
        6. Data reduction
4. DynMR - EuroSys 2014 - IBM
    - Reduce tasks preempt map tasks when there is enough data to shufﬂe
    - Workload:
      - Terasort
      - Tarazu: optimizing MapReduce on heterogeneous clusters

## MapReduce On Heterogeneous Clusters

1. Tarazu - ASPLOS 2012
    - Hadoop Version < 1.0
    - **Key reasons** for MapReduce’s poor performance on heterogeneous clusters:
        1. Map-side: numerous remote Map tasks cause network overhead.

            **_(Not sure still exist in Hadoop Yarn)_**

        2. Reduce-side: equal distribution creates load imbalance

            ***(What about in pre-fetching?)***

    - Tarazu address the above performance problems.

2. Ant - TPDS 2017
    - A self-adaptive tuning approach for task conﬁguration in heterogeneous environments.
    - Task-level parameters:
      - *io.sort.factor*
      - *io.sort.mb*
      - *io.sort.record.percent*
      - *io.sort.spill.percent*
      - *io.ﬁle.buffer.size*
      - *mapred.child.java.opts*
    - Key designs:
      - Tasks belonging to the same job run with different conﬁgurations
      - Dynamically change to search for the optimal settings
    - Groups nodes with similar hardware conﬁgurations or capabilities together

## Data Skew

- Skew in Hadoop
  - Hash partition function(default in Hadoop) works well when the data is uniformly distributed, but can perform badly when the input is skewed (*some key values are signiﬁcantly more frequent than others, e.x. sort benchmark*)
  - Hadoop's solution: a pre-run sample of the input
  - Hadoop's ***speculative execution*** can not solve data skew

1. LIBRA - TPDS 2015
   - Run sample tasks
   - Make the partition decision and then notify the workers
   - Consider heterogeneous clusters: partition ratio
   - **The first data skew mitigation strategies which take *heterogeneity* into consideration**
   - Experiments:
     - Comparing LIBRA with:
       - Hadoop hash partition
       - Hadoop range partition
       - some application speciﬁc partition methods
       - *SkewTune*
     - Workload: generate input following the *Zipf* distribution