---
layout: post
title: "No False Negatives: Accepting All Useful
Schedules in a Fast Serializable Many-Core System"
date: 2020-07-27
---

### Paper ###

**[No False Negatives: Accepting All Useful Schedules in a Fast Serializable Many-Core System](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=8731610)**
<br />
    Dominik Durner and Thomas Neumann. In 2019 IEEE 35th International Conference on Data Engineering (ICDE). 

### Background ### 
Concurrency control (CC) protocols are theoretically based on *conflict serializability*, that is, finding schedules equivalent to a serial schedule with the same read-write, write-write, and write-read data item access pairs. 
Implementing serializability efficiently is challenging and widely used CC protocols each have their drawbacks. 
Locking performs well on highly contended workloads, but does poorly in read-only dominant workloads. 
Timestamp ordering performs well on lowly contended workloads, but suffers in highly contended workloads resulting in unneeded aborts; optimistic CC (OCC) has similar characteristics, scheduling many aborts.
Moreover, these CC protocols do not scale well on modern many-core hardware, e.g., OCC requires an exclusive verification phase, which leads to high contention on this phase and poor overall performance. 
Additionally, modern systems experience mixed OLTP (short-lived read-write transactions) and OLAP workloads (long-running read-mostly transactions), with traditional approaches again performing poorly on these workloads, thus, systems use multi-version CC and relaxed isolation levels, e.g., snapshot isolation, to achieve performance.

### Main Idea ### 
Graph-based CC, or serialization graph testing (SGT), has theoretically optimal properties, accepting all conflict serializable schedules, therefore avoiding unnecessary aborts; other approaches are approximations to this class of schedules, hence, reject some conflict serializable schedules. 
Historically, SGT was deemed impractical due to the cost of maintaining an acyclic graph and the cost of cycle checking - this paper refutes this claim. 
They present a highly parallelizable graph structure that avoids taking an exclusive certification “lock” on the graph, thus, scaling well on many-core architectures. 
They cater for mixed workloads with a read-only multiversion concept for long running read queries.

### Theory ### 
Two algorithms are presented: 
+ **Single-version SGT.** A SGT certifier in which transactions optimistically execute and commit iff they have no incoming edges in the graph, otherwise, an offline cycle check is scheduled and commitment is delayed. To scale well with many-core hardware, a highly parallelizable, node-level locking structure is used to control access to the graph. Nodes are locked in shared mode for edge insertions and cycle checks, with an exclusive lock taken for the commit critical check of no incoming edges. To detect conflicts additional access meta-data is stored for each data item.
+ **Multi-version SGT.** An extension to support read-only transactions in “mixed” OLTP/OLAP workloads. Each row is snapshotted before a write and is assigned an epoch value, which is used to determine the row a read-only transaction needs to access. OLTP-style transactions access the base table/leading edge and use the single-version SGT described in 1. 


### Evaluation ### 
Evaluation uses a prototype database with all data stored in main memory; a NUMA server with 4 processors, with a total of 60 cores and 1024GB DRAM is used. 6 concurrency control protocols were implemented: SGT with offline DFS (S-SGT), SGT with online topological ordering (O-SGT), multi-version SGT with offline DFS (M-SGT), predicate multi-version OCC scheduler (MVOCC), timestamp-based approach (TicToc), and two-phase locking with wait-die deadlock prevention (2PL). 
They ran 4 benchmarks, SmallBank-OLTP, Smallbank-OLTP/OLAP, YCSB, and TATP, measuring comparative throughput, latency, and abort rate under, (i) high contention, (ii) medium/low contention, and (iii) mixed OLTP/OLAP workload. Also, space and time requirements of using graph-based CC were evaluated. 

### Key Results ### 
+ **SGT performed best under high/medium contention.** Used SmallBank-OLTP benchmark with 100 (1000) tuples for high (medium) contention. SGT achieved the highest throughput and the lowest abort rate; MVOCC performed the worst. Average latency was consistent across protocols. Performance for M-SGT dropped slightly, indicating managing multiple versions is not “free” (see Fig. 4 below). 
+ **M-SGT performed best on a mixed OLTP/OLAP workload.** Used SmallBank-OLTP/OLAP, which includes a table scan transaction. 
TicToc had the best OLTP throughput but was unable to commit any OLAP transactions, MVOCC had the best OLAP throughput but was unable to commit any OLTP transactions. 
M-SGT’s performance was nicely balanced between OLTP and OLAP performance (see Fig. 6).
+ **No unexpected aborts.** 
Used TATP benchmark, which generates few conflict cycles, SGT experienced few aborts, whereas 2PL and MVOCC experienced more as any concurrent write access to the same data element, unnecessarily, results in an abort. 
+ **Overhead of maintaining the graph is marginal.** 
Found the CPU overhead needed for cycle checking was a small amount of the total transaction costs. 
Additionally, the overhead of maintaining access history, conflict detection, cycle checking, and aborts was consistent with costs associated with other CC protocols. 
Lastly, maintaining the access history added a small space overhead, e.g., for the YCSB benchmark the memory footprint increased by 2.4%. 

![image info](fig4.png)