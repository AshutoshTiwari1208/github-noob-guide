![git](https://www.cloudsavvyit.com/p/uploads/2019/10/e713ed70-1.png)

## Git Notes for Noobs 🔥

***
#### **COLLABORATE** 🥳
1. Fork the repo.
2. Do changes in forked repo.
3. Raise pull request.

**NOTE:** Please only add notes/formatting! Do not remove any existing statement in the file

***
This Guide will be mentioning the useful commands straight to the point rather than dangling around ! 😃👍

 **To set your identity :**

``` js
> git config --global user.name Ashutosh
```


``` js
> git config --global user.email ashutosh3309@gmail.com
```

> now, while committing (saving) changes these details will be taken ✌️


---

**Message must be in present tense - just like giving order to someone***
``` js
> git commit -m "add e in app.js"
```
> -m is for message !
---

***Another way of commiting***
```
> git commit
```
*☝️ This will open up an editor which will ask for commit message
By default it will be some local editor, --> it's better to change it to VS Code*

---

- Changing git editor to VS Code 👇
``` js
> git config --global core.editor "code --wait"
```
code denotes VS Code here (In case code is not in path -> just goto VSCode -> ctrl+shift+p)--> write "code" --> and click link to path

---

**Oh! you committed some changes and now want to change it !**

```
> git commit --amend
```
- Before ammend command, you can add some file to be added to latest commit
- Also you will get a chance to change the latest commit message.

---

- Use .gitignore to ignore files from getting scanned by git.
eg. 
```
*.js
node_modules/
```
---
**NOTE** Dont initialize git inside already present git repo !! ( Confirm by `git status`)
---
---
***🎋 BRANCHING***

default branch is master/main

To check all branches available
```
> git branch
```
  **master*
***

To make a new branch
```
> git branch <branch_name>
```
eg. > git branch develop

☝️ this will create a new branch=> develop

=> **now at this point head points to both =>  master and develop branch.**

Switching to other branch :
```
> git switch develop
```

NOTE: all commits in a branch will always be in that branch only, other branch have no effect.

---

NOTE:
```
> git checkout master
```
- checkout is same as switch.
-  Checkout has some more features.
- Switch is new way of checkout, switch only focus on changing branches

***

HOW TO CREATE BRANCH AS WELL AS CHECKOUT/SWITCH INTO IT.
``` js
> git switch -c "feature"
```
**-c**

#### OR

``` js
> git checkout -b "feature"
```
**-b**

---
PROBLEMS WHILE CHECKING OUT


- Modified files must be commited, removed or stashed before changing branch if you are switching to file which already have it.
- Untracked Files will follow you to all branch you checkout till commited.
- Always commit or remove changes from branch before you switch.

***

#### DELETING Branch

```
> git branch -d new-testing
```
*-d*

😮 You shouldn't be on the branch which you are deleting 
In case there were some changes, we have to forcefully delete it -> use -D flag instead.

***

#### RENAMING Branch

```
> git branch -m testing1
```
*you should be on the branch to rename it*

---
#### MERGING BRANCHES

1. We have 2 branches:
- Master
- develop

We did 2 commits in master then we create develop branch and did 2 commits in develop branch.
Now to merge develop into master --> we first have to goto branch **where we want to recieve the change** 💯

```
> git checkout master
```

```
> git merge develop
```

NOTE: As after creating branch and doing commits in develop we didn't do anything in Master branch.
So, while merging the head from master just shifted 2 commits forward done in develop.

It's just commits added and there was no change in master.

☝️ These type of merging is called as **Fast Forward Merge** 

- Simple type of merging

Means, just the new commits got added(from where the changes were started) in the master branch after merging.


We went to master and merged Bugfix into it 


Master starts pointing to that hash! So both branch are now pointing to same hash
It's similar to just creating more commits from master (as if we didn't create the new branch)



---
CONCEPT REGARDING git

HEAD always refer to some branch at any given time.
👉 Inside .git < check head file to see the current reference.

/ref/master

go inside the ref folder and master there the file would be pointing to some hashCode which will be the latest commit in that branch

---
**RECURSIVE MERGING**

From Master we took bugfix branch

We did one commits in bugfix.

When going to merge in master we saw master had 1 commits from where we took the branch bugfix.

Now, the git will follow **recursive strategy** to merge the bugfix into master.

Automatic 1 extra commit (merge commit) will be done by git to merge both branch changes.

Merge branch "bugfix"


---

#### MERGE CONFLICTS


Let's say we made a branch and started working on file A
on a different file on same file someone worked on same line of code.

When we go forward to merge => we see Conflicts...

MEANS, files are not merged!

Rather files are staged and file with conflict are not staged!

The unstaged file has conflicts and we need to remove the marker and keep the desired state.
Now just add and commit with message merge ! Done !

---


#### STASHING



```
> git stash
```
this command will save all worked in staging area !
It won't commit it but will save it so can be reused when ever required.


To bring back staged changes
```
> git stash pop
```
This will apply the changes which were saved to the working directory and will remove it from the stash (delete it from there)


In case we want to apply the stash to multiple branches or we don't want to get it deleted =>  then just use "apply"
```
> git stash apply
```
***

**MULTIPLE STASH**


```
> git stash
```

```
> git stash
```

```
> git stash
```

this will create multiple stash!

While popping **most recent** will be popped out.


To check all stash present
``` 
> git stash list
```
*stash@{0}: WIP on develop: 462c835 add master file* **<= specifies branch and commit**

stash@{1}: WIP on develop: 812c982 remove file


To get specific stash, do = > 
```
> git stash apply stash@{2}
```


To remove specific stash
```
> git stash drop stash@{2}
```


To remove everything from stash
```
> git stash clear
```


---


#### UNDOING CHANGES &  TIME TRAVELLING



Let's Timetravel back to some commit using git checkout <commit_hash>

```
> git log --oneline
```
*6dac59f (HEAD -> master) added master-4*

*8edbd21 added master-3*

*1cf5e35 added master-2*

*462c835 add master file with a*

**HEAD** always points to some branch -> branch always has reference to latest commit! **<-- Important!**

We can take HEAD to some commit --> that state would be abnormal as HEAD always points to branch and not commit!
LET's DO IT !


Let's go to commit 1cf5e35   and see the directory at that time how it looked !

```
> git checkout 1cf5e35
```
Note: **switching to '1cf5e35'.**

*You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.*

..
If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. 

__Example__ : 

  ```git switch -c <new-branch-name>```

Or *undo this operation* with:

  ```git switch -```

Turn off this advice by setting config variable advice.detachedHead to false

Now HEAD is in detached  head -> means the abnormal state as the HEAD now doesn't point to any branch --> rather a commit !!

Now, we can see the condition of our work at this commit !!


Now, we can also revert back to Master branch or can create a new branch from this commit !

1. To revert to a Master branch
```
> git checkout master
```

2. Creating a new branch from current commit and start working there!
```
> git checkout -b new-branch
```
Now , we are in new-branch! (We can create changes from 1cf5e35  here in this branch.


In total, now we have 2 branches Master and new-branch ! 
And HEAD is now in attached state as it's pointing to new-branch !

---

JUMPING TO PREVIOUS COMMITS BY JUST NUMBER

	HEAD~1, HEAD~2....


Let's say we want to jump to previous commit from where we are

```
> git checkout HEAD~1
```
Jumps to previous commit

To jump back 2 commits

```
> git checkout HEAD~2
```


Now, as we do it, HEAD points to a commit (Abnormal Condition)- Detached State


Now, in case we want to go back to the latest commit from where we jumped back
```
> git checkout -
```
OR
```
> git switch -
```


---

DISCARD ALL CHANGES DONE ! 


```
> git checkout HEAD .
```

OR

```
> git checkout -- .
```


you can also specify some specific files
```
> git checkout HEAD app.js index.js
```


```
> git checkout -- app.js index.js
```

It won't remove the staging area changes
To unstage all changes
```
> git restore --staged .
```
restore --staged

```
> git checkout -- .
```

---

This work of checkout can be done by restore too !!

```
> git restore .
```
This will remove all changes and take repo to latest commit.


This will take app.js to one commit back !
```
> git restore --source HEAD~1 app.js
```




---
RESETTING COMMIT | REMOVING COMMITS | Deleting Commits


To remove commits and jump to some commit back
```
> git reset 8edbd21
```
This is soft reset => here the changes which were done after this commit will be there as "unstaged"

To remove last commit
```
> git reset HEAD~1
```

to delete commit and jump back to some commit without taking the changes done after the commit 
```
> git reset --hard HEAD~1
```
hard => this won't keep changes which were done after that commit.


---

REVERTING COMMIT  | UNDO A PARTICULAR COMMIT | DOESN't DELETE COMMIT


What if you have done a wrong commit and now want to remove it ?
Going for reset is not a great option
As DELETING HISTORY is ok for your machine but everywhere it won't delete the HISTORY and so  HISTORY MISMATCH may occur.

So Rather Revert a commit.
It will remove all changes done in that commit and will create a new commit where it says "revert <this> commit"

HOW TO DO IT ?

```
> git revert 462c835
```
This will remove changes done in 452c836 and will create a new commit saying it reverted this change.

So for collaboration, revert would be better if changes are already on github.
As deleting history won't be a great option then !!!

---

USING GITHUB

Github is just a cloud service to keep your git repositories and collaborate with others.

To bring a repo on github to your own system ---> clone it !

Clonning a Repo
```
> git clone <url_of_repo>
```
This url can be of any repo hosted online, taking from github is not the only option !

- This will bring the repo
- The logs
- Create remote origin for you

Let's say we want to take the repo online
```
> git remote add origin <url_to_push_repo_to>
```

Now remote is added (Remote is just a name for the url)
```
> git remote -v
```
==> this will list out all your repo's.


To push master into master of repo (If master doesn't exists, it will be created in remote repo)
```
> git push origin master
```

Pushing develop into master
```
> git push origin develop:master
```
==> this will push the develop branch of local to master branch of remote.

---

git push -u



```
> git push origin master
```
We are saying git to push master branch to origin address here
As only master is given means push local master branch to remote master branch.

So, each time we are doing the same command !!
To let git know that for pushing remember to push master into master of remote use -u

```
> git push -u origin master
```
Now, git will remember to push master into master

```
> git push
```
This will now push the master and we don't need to give full command ! 😃

So, we setting the upstream basically here.

---
All branches don't come => git clone .....


only default branch comes in local git repo.

Rest of the remote branches are shown when you do:
```
> git branch -r
```
origin/develop
origin/cat
origin/bugfix
=> Now let's say we want develop branch to work on and want it to track origin/develop


```
> git switch develop 
```
This will make develop branch ... switch to it....... which will be tracking origin/develop !


---
git fetch


This will get all latest info from the remote repo and put it down in the remote/branch <- here and not in the workspace.
We can then merge to the remote branch and get the latest updates!

```
> git fetch
```
-- by default it will fetch origin

```
> git fetch upstream
```

For updating only some branch
```
> git fetch upstream develop
```
-- it will only update upstream/develop branch

---

git pull

git pull will do exact same thing as git fetch + it will merge the changes to our local branch.

So git pull  = git fetch + git merge



```
> git pull origin master
```
-- here you have to provide the branch name! As that will be merged to your current branch!

SHORTER SYNTAX FOR PULL
```
> git pull
```
by default it's origin
by default it takes the branch you are on as obviously you will pull the same branch!
-- But if it's not the origin then you need to type > git pull upstream master

---
README.md

Always add a README file to your repo to tell about the project & how to collaborate etc.

Keep README to the root !

README.md ---> its a MarkDown file, it's just a text to HTML conversion tool !
