# CPSC538B Draft Proposal

Idea: P2P Wikipedia
Specifically: Information retrieval and document linking in P2P networks

## Overall Goal
Create a P2P app that lets you read, create, revise and delete Wikipedia style
documents. The topology should be 100% P2P with an strong emphasis on fast document
retrieval (likely by maintaining some global state) and semantics (hyperlink analogue).
Secondary concerns include document availability (replication), revision conflicts while
tertiary concerns are document storage.

## Focus
1. Fast document retrieval
2. Semantics/how to store pointers to content within documents


## Challenges
 1. Searching for documents
 2. Linking documents (some analogue of hyperlinks)
 3. Protocol to support the above to points

## Assumptions
 1. The part of server component of app is already done (i.e. CouchDB); need to implement client
and server components required to handle "DNS" stuff

## Tasks
### Research
1. Distributed hash tables (DHT), Chord and Content Addressable Networks (CAN)
2. Semantic peer-to-peer networks
3. Outline protocol (how to resolve ID to IP address for http; how to initiate a search)

### Programming - Pass 1
1. Implement "fast document retrieval" algorithm in GO (possibly a DHT table)
2. Implement app protocol (to get address info -- actual communication via http/REST)
2. App UI (at least to view documents). I expect that this will largely just be
an html library for GO.
3. Setup up CouchDB.

### Programming - Pass 2
1. Implement performance monitoring + log visualization
2. Replace CouchDB with own implementation (if required, time permitting)
