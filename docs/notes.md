## Document Phases
1. Creation
2. Propagation
3. Revision (multiple revisions at same time or during propagation i.e. merge conflicts)
4. Removal

## System Phases
- Replication (how to choose which nodes to copy the document too)
- index creation (MapReduce)
- searching index

## System Requirements
- High availability
-


## Challenges:
- document discovery (esp. newly created documents)
- propogating updates
- availablility (never want a document on only 1 node; probably should be available in every geographic region)
  - make available unpopular articles
- indexing content
- **Searching** for content (There are 10 different algorithm in Survey of search and optimization of P2P networks)
- identifying/addressing nodes


## Other Ideas
- Multicast documents: when user A requests a document that happens to be on node X, leave the
document on every node between node X and user A.
- people in the same geographic region may look at the same documents (e.g. for class, cultural, etc)
- eliminate cost of ownership to wikimedia (i.e. their fundrasiers are mostly to host servers)


## Algorithms
 1. Distributed search currently uses the Distributed Hash Table (algorithm has many problems)

## Potential References
- Survey of search and optimization of P2P networks, Cai Kang (DOI: 10.1007/s12083-010-0082-2)
  1. Introduction
  2. Architectures and basic searching algorithms of P2P network
    1. Centralized architecture and its basic algorithm
    2. Distributed structured architecture and its basic algorithm
      - DHT
      - Chord, CAN (Content Addressable Networks)
    3. **Distributed unstructured architecture and its basic algorithm**
      - Gnutella
  3. Advanced searching algorithms
    1. Hybrid P2P search
    2. Iterative deepening
    3. Modified BFS
    4. Directed BFS
    5. Intelligent BFS
    6. Local index
    7. Random walks search
    8. Search based on mobile agents
    9. Routing indices
    10. Adaptive probabilistic search
    11. BubbleStorm search
  4. P2P searches base on intelligence optimization
    1. Resource search based on genetic algorithms
    2. Resource search based on ant colony algorithm
- Friendships that Last: Peer Lifespan and its Role in P2P Protocols
- P2P Networking: An Information-Sharing Alternative (High-level paper)

## Further Research
- [Semantic P2P networks](https://en.wikipedia.org/wiki/Semantic_P2P_networks)
 >Semantic P2P networks are a new type of P2P network. It combines the advantages of unstructured P2P networks and structural P2P networks, and avoids their disadvantages.
 In Semantic P2P networks, nodes are classified as DNS-like domain names with semantic meanings such as Alice @Brittney.popular.music. Semantic P2P networks contains prerequisite virtual tree topology and net-like topology formed by cached nodes. Semantic P2P networks keep the semantic meanings of nodes and their contents. The nodes within semantic P2P networks can communicate each other by various languages. Semantic P2P network can execute complicated queries by SQL-like language.
There are similarities between semantic P2P systems and software agents. P2P means that entities exchange information directly without a mediator. Semantic is a concept to add meaning to information. Peer are usually autonomous systems as well as agents. Agents follow a goal, though. Such goal attainment requires a knowledge base and rules and strategies. That's the major difference between software agents and semantic peers. The later lacks that kind of intelligence.

- [List of P2P protocols](https://en.wikipedia.org/wiki/List_of_P2P_protocols)
-  In contrary, it is possible for a few peers to cheat others with some false or obsolete resources [1, 2].
  1. Wallach DS (2002) A survey of peer-to-peer security issues. In: Proceedings of the international symposium on software security, Tokyo, pp 42-57
  2. Feldman M, Papadimitriou C, Chuang J, et al (2004) Free riding and whitewashing in peer-to-peer systems. In: 3rd annual workshop on economics and information security, pp 228-236
