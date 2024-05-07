# Dependency Graphs

A program's dependencies can be formally described via a what is known in mathematics as a dependency graph. In such a graph, each file is represented by a node, which, when applicable, is annotated with the commands to build it. Dependencies are indicated by arrows (i.e., directed edges) between nodes. If there is an arrow from file A to file B (A → B), then A depends on B, meaning changes to B require A to be rebuilt. If A → B and B → C, then A is indirectly (or transitively) dependent on C. A change to C requires B to be rebuilt, which in turn requires A to be rebuilt.  A dependency graph for our `testintmath` program is shown in Figure 12.3.&#x20;

<figure><img src="../../.gitbook/assets/Group 125 (1).png" alt="" width="563"><figcaption><p>Figure 12.3: testintmath's dependency graph</p></figcaption></figure>

