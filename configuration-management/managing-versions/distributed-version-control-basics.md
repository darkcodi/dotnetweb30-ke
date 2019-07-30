# Distributed Version Control basics

1.       Clone

Create a new repository instance that is a copy of another.

2.       Push

Copy changesets from a local repository instance to a remote one.

![](../../.gitbook/assets/image%20%2838%29.png)

3.       Pull

Copy changesets from a remote repository instance to a local one.

![](../../.gitbook/assets/image%20%28117%29.png)

![](file:///C:/Users/plapt/AppData/Local/Temp/msohtmlclip1/01/clip_image002.png)

4.       Directed Acyclic Graphs \(DAGs\)

In order to support the ability to push and pull changesets between multiple instances of the same repository, we need a specially designed structure for representing multiple versions of things. The structure we use is called a Directed Acyclic Graph \(DAG\), a design which is more expressive than a purely linear model. The history of everything in the repository is modeled as a DAG.

![](../../.gitbook/assets/image%20%2874%29.png)

