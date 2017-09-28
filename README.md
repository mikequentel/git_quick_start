# Git Quick Start and Intro (in my own words).

## About Git
* Unlike older, centralised version control systems, Git is "distributed". What this really means is that there typically is not just one "repo" (repository) of the source code to be stored; instead, there is a local repo on your workstation (PC or laptop or whatever you are working on), and a remote "master" repo that typically lives in a Git repository server, such as GitHub.com
* Additionally, there may be another copy of the repo on GitHub that is either a "fork" (copy) of your repo; or maybe your repo is a fork of someone else's repo. This happens when a repo is popular--people fork the repo and therefore create their own, newer version, independent of the original.
* There are ways to keep the remote repo, the parent fork (or child forks), as well as the local repo, all in sync.
* This is a diagram of the typical workflow of repos, including forks, in GitHub.

```


          github.com server-side repos
  +-------------------+      +------------------+
  |  Source Repo      |      |My fork of Source |
  |-------------------| fork |------------------|
  |                   +----->|                  |
  |                   |<-----+                  |
  +-------------------+ pull +----+-------------+
                        request   |         ^ push
  xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx|xxxxxxxxx|xxxxx
                                  |clone    |
          local hard drive repos  |         |
                                  v         |
                             +--------------+----+
                             |clone of fork      |
                             |-------------------|
                             |<<lots of commits>>|
                             |                   |
                             +-------------------+
 ```

## Clone an existing repo
* This is one of the most common actions you will do: "clone" (download) an existing repo.
* Syntax: `git clone <URL of repo>`
  * Example: `git clone https://github.com/mikequentel/rgb_hsv.git`
* or, you might see this other syntax: `git clone <SSH string>`
  * Example: `git clone git@github.com:mikequentel/rgb_hsv.git`
* When you clone the repo from the server to your workstation, the successful result will be a copy of the repo that is its own, standalone repo.
* The cloned repo can be independently developed, apart from the "remote" (parent) on the GitHub server. Later, the user can do a "push" (upload) to the "remote".

## Create a brand new repo
* This is how you create a new repo.
1. Create in GitHub a new repo.
2. Create the repo using the command `git init` in the parent directory of your source code.
3. Connect this local repo to the one in GitHub so you can push and pull changes between your local repo and the master remote repo: `git add remote <URL or SSH string of repo>`
4. Add the existing source code directory: `git add .`
5. Commit the changes and include a message: `git commit -am "Initialise new repo."`
6. Push the changes to the remote master: `git push -u origin master` (the `-u` is only needed the first time you push in order to link the remote master to your local master; after that, you can simply do `git push origin master`).

## Working with the repos
### `master` and other branches
* On your own projects, you can typically get away with only working in your `master` (default) branch; however, you might want to create a separate branch to fix bugs or create new features.
* If you have more than one branch (more than just `master` branch), then to switch from `master` to another branch, do: `git checkout <name of branch>`
* If you would like to create a new branch, do: `git checkout -b <name of new branch>`
* If you want to switch back to `master`, same sort of syntax: `git checkout master`
### Example of initial commit and push to the remote `origin master`

```
mikequentel@reliance:~/mq/mq_wkspc/git_quick_start$ git remote -v
origin	git@github.com:mikequentel/git_quick_start.git (fetch)
origin	git@github.com:mikequentel/git_quick_start.git (push)
mikequentel@reliance:~/mq/mq_wkspc/git_quick_start$ git branch
mikequentel@reliance:~/mq/mq_wkspc/git_quick_start$ git status
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	README.md

nothing added to commit but untracked files present (use "git add" to track)
mikequentel@reliance:~/mq/mq_wkspc/git_quick_start$ git add .
mikequentel@reliance:~/mq/mq_wkspc/git_quick_start$ git commit -am "Add directory containing README.md"
[master (root-commit) 314253a] Add directory containing README.md
 1 file changed, 54 insertions(+)
 create mode 100644 README.md
mikequentel@reliance:~/mq/mq_wkspc/git_quick_start$ git push -u origin master
Counting objects: 3, done.
Delta compression using up to 2 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 1.68 KiB | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To git@github.com:mikequentel/git_quick_start.git
 * [new branch]      master -> master
Branch master set up to track remote branch master from origin by rebasing.

```

### Example of creating a new branch, then switching back to `master` branch
```
mikequentel@reliance:~/mq/mq_wkspc/git_quick_start$ git remote -v
origin	git@github.com:mikequentel/git_quick_start.git (fetch)
origin	git@github.com:mikequentel/git_quick_start.git (push)
mikequentel@reliance:~/mq/mq_wkspc/git_quick_start$ git branch
mikequentel@reliance:~/mq/mq_wkspc/git_quick_start$ git status
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	README.md

nothing added to commit but untracked files present (use "git add" to track)
mikequentel@reliance:~/mq/mq_wkspc/git_quick_start$ git add .
mikequentel@reliance:~/mq/mq_wkspc/git_quick_start$ git commit -am "Add directory containing README.md"
[master (root-commit) 314253a] Add directory containing README.md
 1 file changed, 54 insertions(+)
 create mode 100644 README.md
mikequentel@reliance:~/mq/mq_wkspc/git_quick_start$ git push -u origin master
Counting objects: 3, done.
Delta compression using up to 2 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 1.68 KiB | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To git@github.com:mikequentel/git_quick_start.git
 * [new branch]      master -> master
Branch master set up to track remote branch master from origin by rebasing.
```
