Git trees are **Merkle trees**.

A Merkle tree calculates the hash of each child node - or each node that is a **leaf**. Then any node that is NOT a leaf - known as an "inode" or "inner node" - calculates the hash of all of its child contents.

https://medium.com/geekculture/understanding-merkle-trees-f48732772199

For example, say we have 8 files in a tree, looking like this:

![[Pasted image 20220908100604.png]]

Then let's say we change the first file, the one indicated by the hash `807db9`. Because of this, the hash of its parent (`33150e`) will change. And the hash of that parent. And ultimately the hash of the root tree. So when we make that change, the tree looks like this:

![[Pasted image 20220908100648.png]]

Notice that all of the nodes on the left of the image have changed, but the rest are unchanged. This allows us to detect changes across incredibly large worktrees without spending forever on traversing through every file. It's one way in which Git is extremely efficient with its filesystem.