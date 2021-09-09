Git is a distributed/decentralized version control system (DVCS)
[Tutorial](https://www.tutorialspoint.com/git/git_basic_concepts.htm)

### Terminology
SHA1: secure hash function

Blob: stands for Binary Large Object. Each version of a file is represented by blob.

Tree: is an object, which represents a directory. It holds blobs as well as other sub-directories. A tree is a binary file that stores references to blobs and trees which are also named as SHA1 hash of the tree object.

Commits: Commit holds the current state of the repository. A commit is also named by SHA1 hash.

**Pull operation** copies the changes from a remote repository instance to a local one.

**Push operation** copies changes from a local repository instance to a remote one. This is used to store the changes permanently into the Git repository. 

## Setup
* Create a local repository in the working directory
```shell
$ git init
```
After this, we will see a hidden folder `.git`

* **Add** files to staging area
```bash
$ git add /path/to/file  # Add a single file
$ git add <folder>/*     # Add all files in this folder
```
After we add files to the staging area, we can view the staged files by
```bash
$ git status -s
```
or `git status -v`. Note when we use `add`, the current version of the file is staged. If we make modification to the file, we need to add it again. 

* **Commit** to local repository.
```bash
$ git commit -m "Comment for the Commit Goes Here..."
```
After commit, we can retrieve this version. 
The next step is **push** to remote repository. 

### Connect to GitHub using SSH.
We first need to create SSH, then copy and paste the public key on our github setting. For the first time connection, do the following in git bash:
```console
$ ls -al ~/.ssh				 # See whether the SSH key exists
$ clip < ~/.ssh/id_rsa.pub	 # Copy the key
$ ssh -T git@github.com        # See whether the connection is successful
```

```bash
$ git remote add origin git@github.com:YuhanLiuSYSU/vertexStateEntanglement.git
$ git remote -v // Check whether it is linked successfully
$ git push origin master
```
