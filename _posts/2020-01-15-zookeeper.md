---
layout: post
title: "ZooKeeper: Wait-free coordination for Internet-scale systems"
date: 2020-01-15
---

### Paper ###

**[ZooKeeper: Wait-free coordination for Internet-scale systems](https://static.usenix.org/event/atc10/tech/full_papers/Hunt.pdf)**
<br />
    Patrick Hunt, Mahadev Konar, Flavio Paiva Junqueira, and Benjamin Reed. In USENIX Annual Technical Conference, 2010.


### Overview ###

Distributed systems often require some of coordination: configuration, group membership and leader election are common examples.

One approach to coordination is to implement services specifically for a given type of coordination. The approach behind ZooKeeper was to build a *coordination kernal* which application developers could then build upon to implement the required type of coordination.

ZooKeeper combines a wait-free hierarchical data structure with operations ordering guarantees (FIFO ordering of client's operations and linearizable writes using Zab) to provide coordination.


### System Architecture and Terminology ###

+ *Client:* a user of the ZooKeeper service.
+ *Server:* a process providing the ZooKeeper service.
+ *Client Library:* exposes ZooKeeper service and manages the network connection between clients and servers.
+ *Session:* established when a client connects to ZooKeeper
+ *Znode:* an in-memory data node.
+ *Data tree:* hierarchical namespace consisting of Znodes.


Data is replicated across servers in the ZooKeeper service. Each server has a request processor it's behavior is dependent on operation type. Writes are forwarded to the leader of the service and Zab is used for agreement across the service. Changes are flushed to disk before changes are made to the server's in-memory data tree. Read requests served by local database; avoiding the agreement protocol and disk I/O. This improves read performance at the cost of stale reads. Servers take periodic snapshots *(fuzzy snapshots)* of the data tree to speed up recovery. Heartbeats are used to detect client failures.

### Applications ###

ZooKeeper is used in Yahoo's Fetching Service, Katta and Message Broker.
