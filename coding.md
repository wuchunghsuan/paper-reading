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