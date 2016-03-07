# Git Basic!!

## Git HELP!
```
$ git help
```

```
$ git help config
```


## Setting up repo
```
$ git config --global user.name "YOUR_NAME"
$ git config --global user.email "YOUR_EMAIL"
$ git config --global color.ui true
```


## Starting a repo
```
$ mkdir store
```

```
$ co store
```

```
$ git init
```



## Add and commit 

Create file (Stats as untracked)
```
$ echo "README" > README.txt
```

To check what's changed since last commit (untracked)
```
$ git status
```

Add file to staging area (Getting ready to take picture)
```
$ git add README.txt
$ git status
```

Commit changes (A snapshot of those on the stage)
```
git commit -m "Create a README"
```

No new or modified files since last commit 
```
$ git status
```

Modify and add file
```
$ echo "Add This" > README.txt
$ touch LICENSE
```

Modified and Untracked status
```
$ git status
```

Add both files to staging area

```
$ git add README.txt LICENSE
```

OR

Adds all new or modified files
```
$ git add --all
```

Check status
```
$ git status
```

Commit!
```
$ git commit -m "Add and modify"
```

Git timeline history
```
$ git log
```


## Git Diff

Show unstaged differences since last commit

* Red : Line removed
* Green : Line added

```
$ git diff
```

Viewing staged differences
```
$ git diff --staged
```

## Unstaging Files

Unstaging Files
```
$ git reset HEAD <file>
```

Discard Changes 
* Reset in to the state that file was in at the last commit, or the last time it was changed
* Blow away all changes since last commit
```
$ git checkout -- <file>
```


## Skip staging and commit (Don't do these after you push!!!)
  
Add changes from all tracked files

* Add any of our tracked files to the stage and then commit them
* Doesn't add new (untracked) files

```
$ git commit -a -m "Modify..." 
```


## Undoing a commit

* --soft : Reset into staging
* HEAD^ : Move to commit before 'HEAD' 

```
$ git reset --soft HEAD^
```

Maybe we forgot to add a file

* --amend : Add to the last commit
* -m "message" : New commit message 
* Whatever has been staged is added to last commit
 
```
$ git add a.txt
$ git commit --amend -m "New Message"
```

Useful commands

Undo last commit, put changes into staging 
```
$ git reset --soft HEAD^
```

Change the last commit 
```
$ git commit --amend -m "New Message"
```

Undo last commit and all changes
```
$ git reset --hard HEAD^
```

Undo last 2 commits and all changes
```
$ git reset --hard HEAD^^
```



## Remots

Adding a remote

* add : New remote
* origin : Our name for this remote (like web browser's bookmark!) 
* last arg : Address  
```
$ git remote add origin https://github.com/yoyojyv/... 
```

Show remote repositories
```
$ git remote -v
```


Pushing to remote

* origin : remote repository name
* master : local branch to push 

```
$ git push -u origin master
```


Pulling from remote
```
$ git pull
```


Working with remotes (Multiple remotes)

To add new remotes
```
$ git remote add <name> <address>
```


To remove remotes 
```
$ git remote rm <name>
```

To push to remotes 

* <branch> usually master

```
$ git push -u <name> <branch>
```



## Cronning & Branching


### Clone

Cloning a repository

* URL : URL of the remote repository

```
$ git clone <URL>
```

or 

* FOLDER : local folder name

```
$ git clone <URL> <FOLDER>
```


Git clone work

- Downloads the entire repository into a new directory
- Adds the 'origin' remote, pointing the clone URL 
- Checks out initial branch (likely master) : sets the HEAD


Show remote repositories
```
$ git remote -v
```



### Branch 

Branching out

* branch created from master
* HEAD still on master 

```
$ git branch <BRANCH-NAME>
```


Show branches 

```
$ git branch
```

Switching to a branch

* HEAD is now <BRANCH-NAME>

```
$ git checkout <BRANCH-NAME>
```

OR

* Using a single command, create and check out.
```
$ git checkout -b <BRANCH-NAME> 
```
 

Merge

* merge brings one branch's changes into another
 
```
$ git checkout master
$ git merge <BRANCH-NAME>
```


Noting was modified on master in the meantime. 

Fast-forward

> Because the commit pointed to by the branch you merged in was directly upstream of the commit you’re on, Git simply moves the pointer forward. 
> To phrase that another way, when you try to merge one commit with a commit that can be reached by following the first commit’s history, 
> Git simplifies things by moving the pointer forward because there is no divergent work to merge together – this is called a “fast-forward.”

>  Merge할 브랜치가 가리키고 있던 커밋이 현 브랜치가 가리키는 것보다 '앞으로 진행한' 커밋이기 때문에 master 브랜치 포인터는 최신 커밋으로 이동한다. 이런 Merge 방식을 'Fast forward'라고 부른다. 


Branch clean up

```
$ git branch -d <BRANCH-NAME>
```


Non-fast-forward

* Git uses VI if no default editor is set to edit commit messages.


Recursive merging

* Git can't fast-forward since changes were made in both branches.


Check log!

* A commit was created to merge the two branches. 

```
$ git log
```




### Collaboration   

If git push rejected...

```
$ git push
```

We could simply do a pull first, and it would work.

```
$ git pull
$ git push
```

Understanding pull

```
$ git pull
```

1. Fetch (or Sync)  our local repository with the remote one (It's samle thing as doing `$git fetch` command)
    * Fetch doesn't actually update any of our local code.
2. Merges the origin/master with master (`$git merge origin/master`)



Merge conflict

```
$ git pull

...
...

CONFLICT (content): Merge conflict in a.txt
Automatic merge filed; fix conflicts and the commot the result.
```

```
$ git status

...
...
#
# both modified:        a.txt 
#

```

Need to edit these (both modified) files. 

open a.txt file and 
```
here is my a.txt

<<<<<<< HEAD
aaa // our local version
======
bbb // other version
>>>>>>>
a123a123123123123123123123312....
```

and edit file and correct 
```
here is my a.txt

aaa
```


commit leave off the message and push    
```
git commit -a

...
...
...

git push
```



### Branching 


Creating a remote branch

* it push origin A_BRANCH : Links local branch to the remote branch (tracking) 

```
$ git checkout -b <A_BRANCH>
$ git push origin <A_BRANCH>
```


Pushing to the branch 

```
$ git add b.txt
$ git commit -a -m "Add b.txt"
$ git push

...
...


To https://github.com/xxx/xxx
    123123...         <A_BRANCH> -> <A_BRANCH>         // Pushed changes from branch                            
```


Pulling new branches

```
$ git pull

... 
...

From https://github.com/xxx/xxx
    * [new branch]          <A_BRANCH>        -> origin/<A_BRANCH>          // Remote branch

```

```
$ git branch
 * master  
```

List all remote branches
```
$ git branch -r
  origin/master
  origin/<A_BRANCH>
```

Checkout
```
$ git checkout <A_BRANCH>
```


Remote show
```
$ git remote show origin
```



Removing a branch 

* `:` => Deletes remote branch 

```
$ git push origin :<A_BRANCH>
```

```
$ git branch -d <A_BRANCH>
  error: The branch '<A_BRANCH>' is not fully merged/
  If you are sure want to delete it, run `git branch -D <A_BRANCH>`
```

Are you sure? 
```
git branch -D <A_BRANCH>
```


On deleted remote branch 

Other user
 
```
$ git commit -m -a "Add some changes"
$ git push                                      // No remote to push to(it's just a local branch now)
```


```
$ git remote show origin
Remote branches:
    master                         tracked
    refs/remotes/origin/<A_BRANCH> stale (use `git remote prune` to remove)
```

To clean up deleted remote branches
```
$ git remote prune origin  
```
 


Tagging

A tag is a reference to a commit (used mostly for release versioning)

List all tags
```
$ git tags
```

Check out code at commit 
```
$ git checkout v0.0.1
```


To add a new tag
```
$ git tag -a v0.0.3 -m "version 0.0.3"
```


To push new tags
```
$ git push --tags
```


git fetch 
> Fetch : only update local branch information
> 중앙 저장소의 소스를 로컬 저장소로 가져온다! 그러나 현재 작업중인 소스들을 변경하는 Merge 작업을 하지는 않는다

git pull
> Pull : pull will auto merge branches 
> 중앙 저장소의 소스를 로컬 저장소로 가져온다! 또한 현재 작업중인 소스들의 Merge 작업까지 통합하여 수행한다

