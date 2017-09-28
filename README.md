# Git Quick Start and Intro (in my own words)
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
* This is how you create a new repo. Here, you will make 1) a remote GitHub repo, and 2) a local repo that will connect with the remote GitHub repo.
1. Create in GitHub a new repo. Could also be GitLab or one of many other Git managers.
2. On your workstation, create the local repo using the command `git init` in the parent directory of your source code.
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
mikequentel@reliance:~/mq/mq_wkspc/git_quick_start$ git branch
* master
mikequentel@reliance:~/mq/mq_wkspc/git_quick_start$ git checkout -b newexamplebranch
Switched to a new branch 'newexamplebranch'
mikequentel@reliance:~/mq/mq_wkspc/git_quick_start$ git branch
  master
* newexamplebranch
mikequentel@reliance:~/mq/mq_wkspc/git_quick_start$ git checkout master
Switched to branch 'master'
Your branch is up-to-date with 'origin/master'.
mikequentel@reliance:~/mq/mq_wkspc/git_quick_start$ git branch
* master
  newexamplebranch
```

### Example of fetching and merging (pulling) from a remote repo into a local repo
```
mikequentel@reliance:~/mq/mq_wkspc/discourse$ git pull
remote: Counting objects: 70453, done.
remote: Compressing objects: 100% (215/215), done.
remote: Total 70453 (delta 17948), reused 18065 (delta 17912), pack-reused 52325
Receiving objects: 100% (70453/70453), 49.65 MiB | 1.58 MiB/s, done.
Resolving deltas: 100% (39710/39710), completed with 3868 local objects.
From https://github.com/discourse/discourse
   2ce9d3d..4319d8a  master     -> origin/master
   1b2a6c6..bad3d4e  beta       -> origin/beta
 * [new branch]      discours   -> origin/discours
 * [new branch]      flexbox-composer -> origin/flexbox-composer
 * [new branch]      hbs-widget -> origin/hbs-widget
 * [new branch]      inline-onebox -> origin/inline-onebox
 * [new branch]      no_timecop -> origin/no_timecop
 * [new branch]      remove-markdownjs -> origin/remove-markdownjs
 * [new branch]      search-log -> origin/search-log
 * [new branch]      sidekiq_mem_leak -> origin/sidekiq_mem_leak
   f7a335a..5137ae8  stable     -> origin/stable
 * [new branch]      super-flags -> origin/super-flags
   9f4ef6e..3e6bf38  tests-passed -> origin/tests-passed
 * [new branch]      translations-aug29 -> origin/translations-aug29
 * [new branch]      upgrade_to_rails_5_1 -> origin/upgrade_to_rails_5_1
 * [new branch]      words      -> origin/words
 * [new tag]         v1.6.10    -> v1.6.10
 * [new tag]         v1.6.2     -> v1.6.2
 * [new tag]         v1.6.3     -> v1.6.3
 * [new tag]         v1.6.4     -> v1.6.4
 * [new tag]         v1.6.5     -> v1.6.5
 * [new tag]         v1.6.6     -> v1.6.6
 * [new tag]         v1.6.7     -> v1.6.7
 * [new tag]         v1.6.8     -> v1.6.8
 * [new tag]         v1.6.9     -> v1.6.9
 * [new tag]         v1.7.0     -> v1.7.0
 * [new tag]         v1.7.0.beta10 -> v1.7.0.beta10
 * [new tag]         v1.7.0.beta11 -> v1.7.0.beta11
 * [new tag]         v1.7.0.beta3 -> v1.7.0.beta3
 * [new tag]         v1.7.0.beta4 -> v1.7.0.beta4
 * [new tag]         v1.7.0.beta5 -> v1.7.0.beta5
 * [new tag]         v1.7.0.beta6 -> v1.7.0.beta6
 * [new tag]         v1.7.0.beta7 -> v1.7.0.beta7
 * [new tag]         v1.7.0.beta8 -> v1.7.0.beta8
 * [new tag]         v1.7.0.beta9 -> v1.7.0.beta9
 * [new tag]         v1.7.1     -> v1.7.1
 * [new tag]         v1.7.10    -> v1.7.10
 * [new tag]         v1.7.2     -> v1.7.2
 * [new tag]         v1.7.3     -> v1.7.3
 * [new tag]         v1.7.4     -> v1.7.4
 * [new tag]         v1.7.5     -> v1.7.5
 * [new tag]         v1.7.6     -> v1.7.6
 * [new tag]         v1.7.7     -> v1.7.7
 * [new tag]         v1.7.8     -> v1.7.8
 * [new tag]         v1.7.9     -> v1.7.9
 * [new tag]         v1.8.0     -> v1.8.0
 * [new tag]         v1.8.0.beta1 -> v1.8.0.beta1
 * [new tag]         v1.8.0.beta10 -> v1.8.0.beta10
 * [new tag]         v1.8.0.beta11 -> v1.8.0.beta11
 * [new tag]         v1.8.0.beta12 -> v1.8.0.beta12
 * [new tag]         v1.8.0.beta13 -> v1.8.0.beta13
 * [new tag]         v1.8.0.beta2 -> v1.8.0.beta2
 * [new tag]         v1.8.0.beta3 -> v1.8.0.beta3
 * [new tag]         v1.8.0.beta4 -> v1.8.0.beta4
 * [new tag]         v1.8.0.beta5 -> v1.8.0.beta5
 * [new tag]         v1.8.0.beta6 -> v1.8.0.beta6
 * [new tag]         v1.8.0.beta7 -> v1.8.0.beta7
 * [new tag]         v1.8.0.beta8 -> v1.8.0.beta8
 * [new tag]         v1.8.0.beta9 -> v1.8.0.beta9
 * [new tag]         v1.8.1     -> v1.8.1
 * [new tag]         v1.8.2     -> v1.8.2
 * [new tag]         v1.8.3     -> v1.8.3
 * [new tag]         v1.8.4     -> v1.8.4
 * [new tag]         v1.8.5     -> v1.8.5
 * [new tag]         v1.8.6     -> v1.8.6
 * [new tag]         v1.8.7     -> v1.8.7
 * [new tag]         v1.9.0.beta1 -> v1.9.0.beta1
 * [new tag]         v1.9.0.beta10 -> v1.9.0.beta10
 * [new tag]         v1.9.0.beta2 -> v1.9.0.beta2
 * [new tag]         v1.9.0.beta3 -> v1.9.0.beta3
 * [new tag]         v1.9.0.beta4 -> v1.9.0.beta4
 * [new tag]         v1.9.0.beta5 -> v1.9.0.beta5
 * [new tag]         v1.9.0.beta6 -> v1.9.0.beta6
 * [new tag]         v1.9.0.beta7 -> v1.9.0.beta7
 * [new tag]         v1.9.0.beta8 -> v1.9.0.beta8
 * [new tag]         v1.9.0.beta9 -> v1.9.0.beta9
First, rewinding head to replay your work on top of it...
Fast-forwarded master to 4319d8a142ea23bdfc9025d137662aa17ac37bd0.
```
