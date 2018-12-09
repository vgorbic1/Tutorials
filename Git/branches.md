## Work with branches
#### How to create a new branch?
```git checkout -b branchname```

#### What is fast-forward merge?
The easiest type of merge. The head is pointing to branch and master (same commit)

#### What is Head?
Head is a marker that points to last commit of current branch

#### How to merge branch with master?
```git merge branchname```

#### How to remove branch locally?
```git branch -d branchname```

#### How to remove a remote branch?
```git push origin :branchname```

#### How to list all local branches?
```git branch```

#### How to list all branches local and remote?
```git branch -a```

#### How to make sure that all remote branches are syncronized with local?
```git fetch```

#### How to push a new branch remotely?
```git push -u origin branchname```

#### How to move to another branch?
```git checkout branchname```

#### How to get updates of all branches at once?
```git pull --all```

#### How to roll back to a previous commits in a history?
```
git reset 8978 --soft // with no destruction
                  --mixed
                  --hard // full return
```
#### How to remove all dead references on remote?
```git fetch -p // means "prune"```
