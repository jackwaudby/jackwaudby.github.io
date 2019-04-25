This markdown file is a scratch space for my blog ideas 

The intention of this blog is to chronicle my journey through my PhD and the world of computer science. 

I started my PhD officially in September 2018. However due to the structure of the Cloud Computing for Big Data CDT I actually choose my project around June 2018, giving me a couple of months head start before the next semester.

Looking back my PhD project choice was a massive leap into the unknown and they probably shouldn't have let me do it, researching distributed graph databases. 

The research decomposes into broadly 3 areas:
1. Distributed Systems 
2. Databases
3. Graph Theory 

In hindsight I didn't realize the scale of the task ahead for me. My undergraduate degree was Economics & Maths, after my first year it was pretty much statistics. Hence, I did my masters in Statistics! The thesis component of my masters was what made me want to do a PhD I really enjoyed, which was largely down to my supervisor, Chris Sherlock, who is awesome. 

My masters thesis ended up being heavily computational and I liked it, but at this point I still knew next to nothing about computers. The first year of the CDT gave me an introduction to computing, we learned about Java, git, python, TDD, the mysterious  cloud, hadoop, spark, neo4j etc. All this convinced me I wanted to transition into computer science. 

I've always liked graph theory ever since the decision module in my maths A-level and I enjoyed playing with Neo4j and learning about several graph algorithms. So when the opportunity arose to do a project in collaboration with Neo4j on building a distributed graph databases I thought: yes, this sounds super cool!! I want to do it!! Let me do it!! Please please please!! and they did. 

Reality check: At this time I knew nothing about database theory, SQL, transactions, ACID, No-SQL. I knew nothing about distributed systems, linearizability, CAP, networks, fault-tolerance. And really I knew nothing about graph theory. But off I went down into the rabbit hole. 

I'm writing this in April 2019, roughly 10 months since I started my PhD and in reflection I have learned a shit ton. 

Key sources of information that have aided my learning have been:
+ You Tube series on distributed systems 
+ Reading academic papers (see papers section)
+ Twitter 
+ Reading some more 
+ Attending modules 
+ Demonstrating on modules

Create a glossary of terms


# Overview of Graph Technologies #

This blog series is an attempt to motivate myself into writing an overview of the graph-based technology space!

When I began my PhD the graph technology space was confusing (and still is), this is my attempt to draw lines in the sand and group technologies into certain buckets. 

A recent [blog post](https://graphaware.com/graphaware/2019/02/01/graph-technology-landscape.html) from [GraphAware](https://graphaware.com) attempted to create a graphic summarizing the graph technology landscape and did a pretty good job. The landscape is broken down into infrastructure, analytics, services, query languages, information resources and conferences. To be included in the landscape technologies had to be "product like" Note, Graphaware are company that specialize in providing training for Neo4j, along with a Neo4j consultancy service and develop some open-source tools that work alongside Neo4j. 

I'm particularly interested in infrastructure and query languages so I'll focus on these areas from now. The blog post breaks infrastructure down into graph databases and graph compute engines, with graph database having 2 further sub-categories "One for graph databases, and one for all other non-native graphy solutions" this is where I hope to add clarity. With respect to query languages I will not discussed them distinctly but more as a feature of the database under question. 


For a while the distinction between a graph database and a graph compute engine was blurry. According to [Graph Databases](https://graphdatabases.com), (co-authored by my PhD co-supervisor Jim Webber) a graph database is used primarily for transactional online graph persistance, normally it is accessed in real time from some application and has create, read, update delete (CRUD) methods - equivalent to a relational OLTP system. The database is optimised for transactional performance and engineered for transactional integrity and operational availability. Whereas, a graph compute engine is equivalent to an OLAP system and is used for offline graph analytics, which is performed as a series of batch steps. This approach enables global graph computational algorithms to be run against large datasets. There is often no graph storage layer and data is fed into from an external source and then the results are returned for storage elsewhere. For example, a system of record database (Neo4j, MySQL etc.) with OLTP properties services requests and responds to users/applications at runtime and periodically data is loaded into a offline compute engine for analysis (Apache Giraph, GraphX). Note, graph compute engines are not graph database management systems - at the time of writing [DB-Engines](https://db-engines.com/en/ranking/graph+dbms) lists Giraph as a graph database, it isn't. 

Now we are going to take a turn away from graph compute engines and focus specifically graph databases. Graph databases can be characterized by many different facets:
+ Does the database have a non-native or native storage layer?
+ Does the database have a non-native or native processing engine? 
+ Is the database replicated or distributed? 
+ What data replication consistency semantics are offered?
+ Are transactions ACID?
+ What query language does the database use?
+ What graph model to the database offer? The labeled property graph or Resource Description Framework (RDF) triples 
+ Is the data persisted to data or stored all in-memory?
+ What range of queries are feasible? Does the 

Disclaimer: my PhD research is focused on distributed graph databases! And I love talking about consistency models. 

We are going to off with JanusGraph

## JanusGraph ###

JanusGraph is an open source distributed graph database, forking from TitanDB in early 2017.

JanusGraph is composed of several building blocks and adapted with a graph layer and query language, see Fig 1. 

It supports various storage backends:
+ Apache Cassandra 
+ Apache HBase
+ Google Cloud Bigtable 
+ Oracle BerkeleyDB

It supports global graph data analytics and ETL via integration with big data platforms:
+ Apache Spark
+ Apache Giraph
+ Apache Hadoop

It also supports geo, numeric and full-text search via external index storages:
+ ElasticSearch 
+ Apache Solr
+ Apache Lucene 

It also has native integration with Apache TinkerPop graph stack, which comprises of Gremlin graph query language, Gremlin graph server and Gremlin applications. And you can visualize graphs stored in JanusGraph vus Cytoscape, Gephi, Graphexp and Linkurious. 












