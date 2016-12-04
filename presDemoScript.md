# P2P Wikipedia Demo
## Setup Details
- Four nodes
  - 1 will act as the server (with IP 127.0.0.1:1111)
  - 1 will be the server's replica (with IP 127.0.0.1:2222)
  - 2 will be clients (so that we can show concurrent inserts) (with IPs 127.0.0.1:3333/4444)

Arrange the four windows (or should there be 6 -- two additional for the client programs)
so that the remote server and its replica are at the bottom and ~1/4 the screen size;
the client servers are at the top and ~1/4 the screen size; the client windows in the
middle and ~1/2 the screen size.

## Node Start Up
- Joining
- Syncing files

## Pull existing article
**Client 1**
```
> p2pwiki 127.0.0.1:3333 article pull chars

Article chars has been pulled successfully from 127.0.0.1:1111.
```

**Client 2**
```
> p2pwiki 127.0.0.1:4444 article pull chars

Article chars has been pulled successfully from 127.0.0.1:1111.
```

**Discussion**
1. Our client program issues a lookup request to its local chord server
2. The local chord server performs a lookup on the network (@Rain how does it do the lookup?)
3. Once the local server has the address of the remote node, it copies the article file
   its local cache using an RPC.

Note: point to the different terminal windows to make it clear what server you
are talking about.

## Look at the article
**Client 1**
```
> p2pwiki 127.0.0.1:3333 article view chars

chars
----
B
D
```

**Client 2**
```
> p2pwiki 127.0.0.1:4444 article view chars

chars
----
B
D
```

**Discussion**
This command walks the local copy of the tree in infix order and displays the
value of each node on a new line. (These are paragraphs)

Notice that both clients have the same article content so we can make potentially
conflicting changes (which we will do now).


## Edit the article
**Client 1**

```
> p2pwiki 127.0.0.1:3333 article insert 1 "A"

chars
---
A
B
D
```
```
> p2pwiki 127.0.0.1:3333 article insert 3 "C"

chars
---
A
B
C
D
```

**Client 2**
```
> p2pwiki 127.0.0.1:3333 article insert 1 "X"

chars
---
X
B
D
```

**Discussion**
Each client inserts the characters along a unique path in the tree. These paths are
unique per client. Each insert command is stored in a client log along with the paragraph
and the path.

Notice that the two clients each inserted a different character in position 1 of
the article. These paths




## Push the article
**Client 1**

**Client 2**

**Discussion**
1. Client lookups the server responsible for the beer article and sends the operation
   log.
2. The remote server replays the log on its copy of the article treedoc, inserting
   concurrent paragraphs (those that have the same path) as side-nodes.


## Pull the article + view
**Client 1**
```
> p2pwiki 127.0.0.1:3333 article pull chars

Article chars has been pulled successfully from 127.0.0.1:1111.
```
```
> p2pwiki 127.0.0.1:3333 article view chars

chars
----
A
X
B
D
```

**Client 2**
```
> p2pwiki 127.0.0.1:4444 article pull chars

Article chars has been pulled successfully from 127.0.0.1:1111.
```
```
> p2pwiki 127.0.0.1:4444 article view chars

chars
----
A
X
B
D
```

**Discussion**
As expected, the article is now the same on both clients. (@Nick make this better)
