---
title: Neo4j Practical
layout: default
---

## {{ page.title }} ##

In today's practical you are going to get some hands-on experience using Neo4j by writing some Cypher queries.

You will interact with a Neo4j instance running on Microsoft Azure via the Neo4j browser. Open a browser and enter the url: <a href="https://52.151.95.57:7473" target="_blank"> https://52.151.95.57:7473 </a>


Login credentials:

* Username: neo4j
* Password: csc8101

Neo4j is loaded with the <a href="http://ldbcouncil.org" target="_blank"> Linked Data Benchmark Council </a> social network dataset. There are ~327K nodes and ~1.47M edges, you can view the schema <a href="https://github.com/ldbc/ldbc_snb_datagen" target="_blank"> here </a> (scroll down to the bottom of the page).

Before attempting the queries you can familiarize yourself with the Neo4j Browser by executing the command below in the prompt:

{% highlight cypher %}
:play intro
{% endhighlight %}

You can find a quick overview on common Cypher statements by executing:

{% highlight cypher %}
:play cypher
{% endhighlight %}

### Query 1 ###

Q1. What language(s) does Jack Wilson speak?

### Query 2 ###

Q2. Find the city and country Jack Wilson lives in along with his email address(es).

### Query 3 ###

Q3. Find the comment(s) made by Jack Wilson that were made when Jack was not in Canada and that are over 70 characters in length.

### Query 4 ###

Q4. Find all of Jack's friends of friends that work in a company located in a country that starts with the letter 'A'. Returns the number of friends that work in each country. E.g. Austria, 89. *Hint: Cypher has a keyword STARTS WITH*


### Query 5 ###

Q5. Find the forum(s) that are moderated by Jack's friends and friends of friends in which Jack has made a post.

### Query 6 ###

The queries you have written so far have been neighborhood queries starting from a single node and matching a pattern in the graph. Neo4j has a handy library for performing global graph analytics e.g. community detection, centrality measures etc.

Q6. Using the graph algorithms library run PageRank over the KNOWS subgraph. Return the top 5 influential people in the network. *Hint: Whilst having direction the KNOWS subgraph actually is an undirected graph, you need to account for this. See Section <a href="https://neo4j.com/docs/graph-algorithms/current/algorithms/page-rank/#algorithms-pagerank-usecase" target="_blank"> 5.1.6 </a>*.


### Next Steps ###

Neo4j provide free online training through their <a href="https://neo4j.com/graphacademy/" target="_blank">GraphAcademy</a>. You can also become a Neo4j certified developer by taking the free <a href="https://neo4j.com/graphacademy/neo4j-certification/" target="_blank"> certification course</a>.

### Cypher style recommendations ###

Here are some Neo4j-recommended Cypher coding standards:
- Node labels are CamelCase and begin with an upper-case letter (examples: Person, NetworkAddress). Note that node labels are case-sensitive.
- Property keys, variables, parameters, aliases, and functions are camelCase and begin with a lower-case letter (examples: businessAddress, title). Note that these elements are case-sensitive.
- Relationship types are in upper-case and can use the underscore. (examples: ACTED_IN, FOLLOWS). Note that relationship types are case-sensitive and that you cannot use the "-" character in a relationship type.
- Cypher keywords are upper-case (examples: MATCH, RETURN). Note that Cypher keywords are case-insensitive, but a best practice is to use upper-case.
- String constants are in single quotes, unless the string contains a quote or apostrophe (examples: ‘The Matrix’, "Something's Gotta Give"). Note that you can also escape single or double quotes within strings that are quoted with the same using a backslash character.
- Specify variables only when needed for use later in the Cypher statement.
