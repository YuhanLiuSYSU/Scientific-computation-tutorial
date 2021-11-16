Git is a distributed/decentralized version control system (DVCS)
[Tutorial](https://www.tutorialspoint.com/git/git_basic_concepts.htm)

### Terminology
SHA1: secure hash function

Blob: stands for Binary Large Object. Each version of a file is represented by blob.

Tree: is an object, which represents a directory. It holds blobs as well as other sub-directories. A tree is a binary file that stores references to blobs and trees which are also named as SHA1 hash of the tree object.

Commits: Commit holds the current state of the repository. A commit is also named by SHA1 hash.

**Pull operation** copies the changes from a remote repository instance to a local one.

**Push operation** copies changes from a local repository instance to a remote one. This is used to store the changes permanently into the Git repository. 


## Connect to GitHub using SSH
### First time: connect to github account
We first need to create SSH, then copy and paste the public key on our github setting. For the first time connection, do the following in git bash:
```bash
$ ls -al ~/.ssh				 # See whether the SSH key exists
$ clip < ~/.ssh/id_rsa.pub	 # Copy the key
$ ssh -T git@github.com      # See whether the connection is successful
```
Note that the ssh key is kept at `C:\Users\yuhanliu\.ssh`. 

### Connect local repository to remote one
* Create a local repository in the working directory
```bash
$ git init
$ git config --global init.defaultBranch main
```
After this, we will see a hidden folder `.git`. In the second line, we set the default branch to main. (Maybe we can use `git init -b main`??)
Having set up the ssh connection, we can now [link the local project to github](https://docs.github.com/en/github/importing-your-projects-to-github/importing-source-code-to-github/adding-an-existing-project-to-github-using-the-command-line). We first need to create a remote repository and obtain its url (git@github.com:YuhanLiuSYSU/vertexStateEntanglement.git)
```bash
$ git remote add origin git@github.com:YuhanLiuSYSU/vertexStateEntanglement.git
$ git remote -v # Check whether it is linked successfully
$ git push origin main
```
In the old version, the default branch is `master`. Here is [a post](https://zhuanlan.zhihu.com/p/339370999) on changing it to `main`.

If there are files already in the remote repository, we need to first **pull** them to local one:
```bash
$ git pull origin main
```

## Add, commit and push
* **Add** files to staging area
```bash
$ git add /path/to/file  # Add a single file
$ git add <folder>/*     # Add all files in this folder
```
After we add files to the staging area, we can view the staged files by
```bash
$ git status -s
```
or `git status -v`. Note when we use `add`, the current version of the file is staged. If we make modification to the file, we need to add it again. `add` can be undo (unstaged) by `reset`:
```bash
$ git reset <file>
```
If we want to ignore a subfolder, we can edit the file `.git/info/exclude` by writing the path of folder that we want to exclude. 

* **Commit** to local repository.
```bash
$ git commit -m "Comment for the Commit Goes Here..."
```
After commit, we can retrieve this version. 

* **Push** to remote repository.
After connecting to GitHub (only need for the first time), we then do:
```bash
$ git push origin main
```
## Switch between branches
```bash
$ git checkout -b branch_one
```
allows us to switch to `branch_one`. If it doesn't exist, git will create it.
## Merge
Before merging two branches, we first need to pull from remote repository.





