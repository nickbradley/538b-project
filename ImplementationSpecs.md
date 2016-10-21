#Implementation Specifications
##Definitions
A `node` is the process that will act as our app.
Properties:
 - Unique ID (how?)

##Article Replication
###Version Vectors
A good introduction to version vectors can be found http://basho.com/posts/technical/vector-clocks-revisited/

A Version Vector is a data structure that summarizes the history of updates to an article. Every article has its own Version Vector. The data structure which is a list of pairs of `Node.ID` and `Counter`.

```
[{Node.ID, Counter}]
```
When a node updates an article it will increment only its own entry in the vector. A node's entry is a summary of all the updates that node has performed. If a node is not present in the vector, its counter is agreed to be at zero. As each entry is a summary of an actors updates, the whole Version Vector summarizes all the updates to the article from all the nodes in the system.

```
A = [{a, 3}, {b, 2}, {c, 1}]
```
In Version Vector **A** three nodes **a**, **b** and **c** have updated an article. Node **a** has issued three updates, **b** two and **c** one.

On its own, this does not tell us much. Version Vectors are usually considered in pairs.
```
A = [{a, 3}, {b, 2}, {c, 1}]
B = [{a, 3}, {b, 2}, {c, 1}]
```
The pair of Version Vectors above are equal; they describe exactly the same set of events or _history_.
```
A = [{a, 4}, {b, 2}, {c, 1}]
B = [{a, 3}, {b, 2}, {c, 1}]
```
Above, **B** is an ancestor of **A**. We say that **A** *dominates* **B**. **A** has seen an extra event `({a,4})` which means its clock shows a later logical time that **B**. You can think of _dominates_ as _greater than_: `A > B`. We can discard all information in **B** since it is contained in **A**. This is more meaningful than just a greater temporal timestamp; with a dominated Version Vector we _know_ for certain that the events in **B** caused **A**. A wall-clock derived timestamp does not convey this information.

_Dominates_ is a stronger relationship than _descends_. For any pair of Version Vectors **A decends B** if **A** summarises all the events **B** does. So the _equal_ Version Vectors descend each other. You can think of _descends as greater than or equal_: `A >= B`. 
```
A = []
B = [{a,1}]
```
In the pair above **B dominates A**. All Version Vectors descend the empty Version Vector, and this single event means **B** summaries events **A** does not.

```
A  = [{a,1}]
B  = [{b,1}]
AB = [{a,1},{b,1}]
```
Merging two Version Vectors takes the pairwise maximum of each entry (as in **AB** above). This merged Version Vector dominates both **A** and **B**. When node **c** issues a new update, it will increment its counter in this merged Version Vector, ensuring the new value overwites both the conflicting values as **ABC** dominates **A**,**B** and **AB**. (We can store the merged Version Vector with the new value as the **frontier**, or latest logical time.
```
ABC = [{a,1}, {b,1}, {c,1}]
```
To summarize: nodes working serially update their own entry in a vector moving logical time forward in discrete events. Conflict, ancestry and dominates can be established by comparing logical clocks for an article.


##Article Discovery
