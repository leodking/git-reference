SHA-1 stands for **Secure Hash Algorithm 1**. It's a cryptographic hash function which was originally used to compress files for security purposes. It is no longer considered secure for cryptography purposes, but it is used by Git instead to uniquely identify **commits**.

In Git, a SHA-1 is created by applying the algorithm to all of the files which are in the source tree, and other data. This produces a unique string for that commit, which is very unlikely to be duplicated. It's a **checksum** - it will come out with the same value every time. The checksum is based on the contents of the commit - so given the same data, you would get the same result.

We label commits by the SHA-1 value, or the "shah" /ʃɑː/ value.

#git