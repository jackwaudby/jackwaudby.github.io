---
layout: post
title: "The Ubiquity of Large Graphs and Surprising Challenges of Graph Processing"
date: 2020-01-24
---

### Paper ###

**[The Ubiquity of Large Graphs and Surprising Challenges of Graph Processing](https://dl.acm.org/doi/pdf/10.1145/3164135.3164139)**
<br />
    Siddhartha Sahu, Amine Mhedhbi, Semih Salihoglu, Jimmy Lin, and M. Tamer Özsu. Proceedings of the VLDB Endowment, 2017.


### Overview ###

This paper aims to address how graphs are used in practice, focusing on 4 areas:
+ Types of graphs
+ Graph computations ran
+ Types of software used
+ Challenges users faces when processing graphs

The authors conducted an online survey (34 questions) of 89 users of 22 different software products. Users were broken down into researchers (36) and practitioners (53). Software products were categorized as graph databases (GDBMSs), RDF engines, linear algebra software, visualization software, query languages and distributed graph processing systems (DGPSs). In addition to the survey, the authors reviewed user feedback in mailing lists, bug reports and feature requests of the software products. They also reviewed academic literature covering 90 papers from 6 conferences.

### Key findings on graph datasets ###

+ Graph represent a wide range of entities: human, non-human (52 kinds), RDF and scientific. Product graphs were the most common non-human entities in practitioner’s graphs. Authors state a product graph benchmark would be useful.
+ Large graphs were common across companies of all sizes and domains - 20 (12P/8R) have graphs with 1B+ edges and 27 (10R/17P) have graphs with 100M+ vertices. When following up with additional users via email, 42 reported graphs with 1-10B edges, 17 with 10B-100B edges, 7 with 100B+ edges.
+ All participants, except 3, reported storing properties on vertices/edges. No breakdown of property type by vertex/edge or number stored on vertex/edge is provided.
+ 40 participants reported having static graphs, 55 reporting having dynamic graphs and 18 streaming graphs (where some information is discarded after some time period).

### Key findings on graph computations ###

+ The most popular computation is finding connected components. Hypothesised as a pre-processing step for further computations.
+ Other types of computations reported were neighbourhood queries, shortest path, subgraph matching, ranking/centrality scores, aggregations, reachability queries, graph partitioning and node similarity.
+ 61 participants use ML on graphs to solve community detection, recommendation system problems and for link prediction. Clustering/classification most popular type of computation.
+ 32 participants reported performing incremental/streaming computations. Although it is unclear what software they use.

### Key findings on type of software used ###

+ GDMBSs most popular. Author’s highlight sampling bias.
+ RDMBSs still used by 21 participants (16 of them also used a GDBMS). Authors suggest a pipeline in which RDBMSs are used for transaction processing then an ETL process into a GDBMS for analytics. This seems the obvious way an enterprise would add graph processing capabilities to their existing pipeline without a major overhaul.
+ Only 6 participants used DGPS, yet it they are heavily studied in academia.

### Key findings on challenges ###

+ User’s find loading, updating, performing computations e.g. traversal on large graphs a bottleneck.
+ Query languages have low expressibility and lack standards compliance. Users want query composition and to be able to query across multiple graphs.
+ Graph visualization is massively important to users.
+ User’s want the ability to process high-degree vertices in a special way.
+ User’s want to add hyperedges, versioning, schema and constraints e.g. graph being acyclic and triggers: adding a property to vertices during insertion to systems.
+ For DGPSs users want more off the shelf algorithms and the ability to generate different types of synthetic graphs, k-regular graphs, random directed power-law graphs.

### Other comments ###

+ The section of on workloads focuses on time taken in certain components of the lifecycle. It would have been interesting to break workloads down by read/write ratio and relative frequencies of query types.
