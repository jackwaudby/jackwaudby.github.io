---
layout: post
title: "Understanding Replication in Databases and Distributed Systems"
date: 2020-08-10
---

### Paper ###

**[Understanding Replication in Databases and Distributed Systems](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=840959)**
<br />
   Matthias  Wiesmann, Fernando Pedone, André Schiper, Bettina Kemme, and Gustavo Alonso.
<br />
   In 2000 IEEE 35th International Conference on Distributed Computing Systems (ICDCS).

I found this paper an excellent read and it helped clarify my understanding of a topic (replication) that can be rather confusing at times.
It is worth noting this paper is, at the time of writing, 20 years old, preceding the development of deterministic databases and the popularity of protocols that provide weaker consistency guarantees, e.g., eventual consistency, CRDTs.

### Contribution ###
The main contribution is a high-level framework for comparing and contrasting replication techniques from the distributed systems and database communities.
Each community uses different terminology and models, makes different assumptions, and focuses on providing different guarantees, which makes comparing protocols a non-trivial task.

### Distributed Systems vs. Databases ###
1. **System model.**
Distributed systems protocols distinguish between the system model being assumed.
The synchronous model assumes there is a known bound on processing speeds and transmission times.
The asynchronous model assumes no bounds are known; here, correct crash detection is a challenge.
Database protocols tend to not distinguish between models in their specifications.
2. **Blocking protocols.**
Databases allowing blocking protocols (a crash can prevent protocol termination), whereas distributed systems opt for non-blocking protocols.
3. **Liveness.**
Database protocols do not formally treat liveness, focusing on safety, e.g., ACID properties are all safety properties.
4. **Operator Intervention.**
Database protocols often allow an operator to intervene to solve abnormal cases, e.g., manual failover.
In distributed systems protocols replica replacement is typically integrated into protocols.
5. **Determinism.**
Distributed systems protocols distinguish between deterministic (same operations in the same order produces the same outcome) and non-deterministic replica behavior.
Databases typically avoid assuming determinism, however, a significant body of research on "deterministic databases" post dates this paper.

### Replication Framework ###
Describes five generic phases:
1. **Client contact.**
An operation is submitted to one or more replicas.
In databases clients never directly contact all replicas.
In distributed systems there are two options, (i) active replication, clients broadcast operations to all replicas, or (ii) passive replication, client contact one replica, which is then forward to other replicas.
2. **Server coordination.**
Replicas synchronise to agree on the ordering of concurrent operations.
In databases the ordering is according to data dependencies as operation semantics are important; correctness criteria is one-copy serializability.
In distributed systems there are strict definitions of ordering, e.g., causality, total order; correctness criteria examples are linearizability and sequential consistency.
3. **Execution.**
Replicas execute the operation.
Note, in all both protocols the operation is only executed and not applied.
4. **Agreement coordination.**
Replicas agree on the result of the execution.
In databases normally use an atomic commitment protocol, e.g., 2PC, for this phase to determine commit/abort decision.
Whilst Step 2 determines the operation ordering it is not alone sufficient as there are numerous additional reasons a transaction can abort.
In distributed systems this phase requires no further checking as the ordering from Step 2 is sufficient.
5. **Client response.**
Client is notified of their operation’s outcome.
In databases there are two approaches to this phase, (i) eager/synchronous, clients do not receive a response until all replicas are updated, and (ii) lazy/asynchronous, clients receive an intermediate response after local execution and updates are propagated to other replicas afterwards.
Distributed systems normally opt for approach (i), however, a significant body of research on “optimistic replication”, e.g., CRDTs, eventual consistency, post dates this paper.

<center>
<img src="/assets/replication_model.png" alt="Functional Replication Model" width="50%">
</center>
