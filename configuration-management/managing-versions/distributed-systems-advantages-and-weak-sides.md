# Distributed systems advantages and weak sides

### CVCS vs DVCS

![](../../.gitbook/assets/image%20%2817%29.png)

![](../../.gitbook/assets/image%20%2890%29.png)

### Advantages of DVCS

1.       Private Workspace  
The concept of a private workspaceis central to all version control tools. Centralized version control systems provide developers with a private place to work by giving them a working copy.

2.       Fast  
Developers usually don’t realize how fast a DVCS can be until they’ve tried one—stuff is really, really fast when most of your operations are against a local repository instance instead of a server. Broadly speaking, developers who switch from \[almost\] any CVCS to \[almost\] any DVCS experience performance gains like these for \[almost\] all daily operations.

3.       Offline  
A developer has to fly across the country and writes some code on the plane. Two hours in, at 31,000 feet, he’s finished his changes and wants to commit them. With a DVCS, this is possible, since he has a repository instance on his laptop.

4.       Geography  
Consider a development team that is split up in two cities. Half the team is in a satellite office in Crabapple Cove, Maine, and the other half is at the company’s headquarters in Ottumwa, Iowa. With a CVCS, they have to pick one city to hold the central server and everybody in the other city has to access it over an Internet link. With a DVCS, they can set up a central server in each city and use push and pull to synchronize them whenever as they want.

![](../../.gitbook/assets/image%20%2844%29.png)

5.       Flexible Workflows  
You might also want to create a repository instance to support a specific purpose. Or you might want to use named branches to manage simultaneous work on more than one release.

6.       Easier Merging  
People using a CVCS tend to avoid branching because most of those centralized tools aren’t very good at merging. When they switch to a DVCS, they tend to bring that attitude with them, even though it’s not really necessary anymore. Decentralized tools are much better at merging.

7.       Implicit Backup  
We get a little extra security knowing that there are dozens more live copies of the whole repository regularly being used on other machines. Any of them could become the central repository on short notice.

8.       Scale out, not just up  
With a DVCS, it is also possible to scale the central server by turning it into a server farm. Instead of one large server machine, you can add capacity by adding more small server machines, using scripts to keep them all in sync with each other.

### Weak sides of DVCS

1.       Locks  
 There isn’t much support for lock in distributed version control.  
 And for some, lock is a critical feature. A great example is a team building a game with lots of graphical assets kept under version control along with the code. With binary files and other cases where automerge cannot work, locking a file is often the right way to go.

2.       Very Large Repositories  
 Having the whole repository on your laptop is fine if it’s a gigabyte. If it’s a terabyte, not so much.

3.       Obliterate  
 Having lots of copies of the data does reduce the risk of losing that data, but it also makes it far more difficult to destroy.

4.       Administration  
 A nice thing about a CVCS is that the repository server provides a nice centralized place to do administration, including security, access control, permissions, management of user accounts, etc.  
 Git and Mercurial are a bit weak in the area of administrative features and user accounts. Both of these tools allow the user to identify himself with any string, and that string is recorded in the repository history.

