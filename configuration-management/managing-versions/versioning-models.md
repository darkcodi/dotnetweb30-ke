# Versioning Models

### The Problem of File Sharing

All version control systems have to solve the same fundamental problem: how will the system allow users to share information, but prevent them from accidentally stepping on each other's feet?

![](../../.gitbook/assets/image%20%2810%29.png)

### The Lock-Modify-Unlock Solution

Many version control systems use a _lock-modify-unlock_ model to address the problem of many authors clobbering each other's work. In this model, the repository allows only one person to change a file at a time.

![](../../.gitbook/assets/image%20%28142%29.png)

### The Copy-Modify-Merge Solution

Subversion, CVS, and many other version control systems use a _copy-modify-merge_ model as an alternative to locking. In this model, each user's client contacts the project repository and creates a personal _working copy_—a local reflection of the repository's files and directories. Users then work simultaneously and independently, modifying their private copies. Finally, the private copies are merged together into a new, final version. The version control system often assists with the merging, but ultimately, a human being is responsible for making it happen correctly.

![](../../.gitbook/assets/image%20%28152%29.png)

Then

![](../../.gitbook/assets/image%20%28131%29.png)

