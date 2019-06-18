# Coding

## [IPDPSW '2017] Coded TeraSort

- Focus on **sorting**
- Goal: Use coding to reduce the data shuffling load, and speed up the overall computations.
- CodedTeraSort
  - a new distributed sorting algorithm
  - impose structured redundancy
  - Fig 1
  - **Use XOR and redundancy task to reduce communication load.**
  - speed up 1.97×- 3.39×

## [TIT '2018]A Fundamental Tradeoff Between Computation and Communication in Distributed Computing

- Goal: Reduce the load of data shufﬂing via coding and some extra computing in the Map phase
- “Coded Distributed Computing” (CDC)
  - Assign computation of each Map task at r carefully chosen nodes (for some r ∈ N), in order to enable in-network coding opportunities that reduce the communication load by r×

## [TIT '2014] Fundamental Limits of Caching

- Caching: to reduce peak traffic in network
  - During off-peak hours, cache the content. Then in the peak hours,  the request can be served from the cache.
  - Shift traffic from peak to off-peak hours
- Two phases:
  - The placement phase: cache the content in off-peak hours
  - The delivery phase: deliver the rest content that not in the cache
- Rate: the load of the shared link normalized by the ﬁle size
  - uncoded: K · (1 − M/N)
  - coded: ...

## [TIT '2017] Improved Lower Bounds for Coded Caching

- content caching
  - store relatively popular content in local memory