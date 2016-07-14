## Git. Basic Knowledge
Git is a software that allows you to keep track of changes made to a project over time. Git works by recording the changes you make to a project, storing those changes, then allowing you to reference them as needed. Check if you already have Git installed:
```
git --version
```
#### CONFIGURE GIT
To configure Git, use the following commands. To set your user name and email:
```
git config --global user.name "Vlad Gorbich" 
git config --global user.email "vlad@example.com"
```
To check what is set in your configuration:
```
git config user.name
git config user.email 
```

#### INITIALIZE A PROJECT 
The command sets up all the tools Git needs to begin tracking changes made to the project.
```
git inint
```
A Git project can be thought of as having three parts:
•	A Working Directory: where you'll be doing all the work: creating, editing, deleting and organizing files.
•	A Staging Area: where you'll list changes you make to the working directory.
•	A Repository: where Git permanently stores those changes as different versions of the project.
 
As you write new code in a project, you will be changing the contents of the working directory. You can check the status of those changes:
```
git status
```
In the output, notice the file in red under untracked files. Untracked means that Git sees the file but has not started tracking changes yet. 

#### ADD FILES TO STAGING AREA
In order for Git to start tracking a project, the file needs to be added to the staging area:
```
git add filename anotherfilename
```
The word "filename" and "anotherfilename" here refers to the name of the files you are editing. In the output, Git indicates the changes to be committed with "new file: filename" in green text. Here Git tells us the file was added to the staging area. To put all files in the current directory to the staging area use:
```
git add .
```

#### CHECK DIFFERENCES IN FILES
Imagine that we type another line in the project code. Since the file is tracked, we can check the differences between the working directory and the staging area with:
```
git diff filename
```
Changes to the file are marked with a + and are indicated in green.

If you need to see the changes between staging area and repository, use this command:
```
git diff --staged
```

#### COMMIT TO REPOSITORY
A commit is the last step in our Git workflow. A commit permanently stores changes from the staging area inside the repository. However, one more bit of code is needed for a commit: the option -m followed by a message. Here's an example:
```
git commit -m "Complete first line of dialogue"
```
Standard Conventions for Commit Messages:
-	Must be in quotation marks
-	Written in the present tense
-	Should be brief (50 characters or less) when using –m

To commit directly from your working area:
```
git commit –am "Message about the commit"
```
This command commits all files in your project directory.

#### LIST YOUR COMMITS
Often with Git, you'll need to refer back an earlier version of a project. Commits are stored chronologically in the repository and can be viewed with:
```
git log
```
In the output, notice:
-	A 40-character code, called a SHA, that uniquely identifies the commit. This appears in orange text.
-	The commit author (you!)
-	The date and time of the commit
-	The commit message

To see commits of a particular author use the beginning of authors name:
```
git log --author="vlad"
```
To see commits in one line:
```
git log –pretty=oneline
```

#### REMOVE OR MOVE PROJECT FILES
In order to remove a file from project use the UNIX command:
```
git rm filename
```
You still need to commit changes to the project.

To rename a file in the project use another UNIX command:
```
git mv filename
```
Again, you need to commit the file to the repository.

#### UNDO CHANGES
When working on a Git project, sometimes we make changes that we want to get rid of. Git offers a few eraser-like features that allow us to undo mistakes during project creation. In Git, the commit you are currently on is known as the HEAD commit. In many cases, the most recently made commit is the HEAD commit. To see the HEAD commit, enter:
```
git show HEAD
```
The output of this command will display everything the git log command displays for the HEAD commit, plus all the file changes that were committed. Notice the output. The most recently added line is in green text.
```
git checkout HEAD filename
```
This command will restore the file in your working directory to look exactly as it did when you last made a commit. Similar command to undo changes that were done in working directory:
```
git checkout -- filename
```
To remove unstaged files:
```
git reset HEAD filename
```
This command resets the file in the staging area to be the same as the HEAD commit. It does not discard file changes from the working directory, it just removes them from the staging area. Notice in the output, "Unstaged changes after reset". M is short for "modification"

To get older versions of the project's files from your repository:
```
git checkout 4427 -- filename
```
4427 is a beginning of the commit token. To find the exact commit token, use git log command.

Git enables you to rewind to the part before you made the wrong turn and create a new destiny for the project. You can do this with:
```
git reset SHA
```
This command works by using the first 7 characters of the SHA of a previous commit. For example, if the SHA of the previous commit is 5d692065cf51a2f50ea8e7b19b5a7ae512f633ba, use:
```
git reset 5d69206
```
To find the proper SHA, first use: 
```
git log
```
To better understand git reset commit_SHA, notice the diagram on the right. Each circle represents a commit. Before reset: HEAD is at the most recent commit. After resetting: HEAD goes to a previously made commit of your choice. The gray commits are no longer part of your project. You have in essence rewinded the project's history:
 
#### BRANCHING
Up to this point, you've worked in a single Git branch called master. Git allows us to create branches to experiment with versions of a project. Imagine you want to create version of a story with a happy ending. You can create a new branch and make the happy ending changes to that branch only. It will have no effect on the master branch until you're ready to merge the happy ending to the master branch.

You can use the command below to answer the question: “which branch am I on?”
```
git branch
```
New Branch is a different version of the Git project. It contains commits from Master but also has commits that Master does not have.

To create a new branch, use:
```
git branch new_branch
```
Here new_branch would be the name of the new branch you create, like photos or blurb. Be sure to name your branch something that describes the purpose of the branch. Also, branch names can’t contain whitespaces: new-branch and new_branch are valid branch names, but new branch is not.

The master and fencing branches are identical: they share the same exact commit history. You can switch to the new branch with:
```
git checkout branch_name
```
You will be now able to make commits on the fencing branch that have no impact on master. Let's switch to the fencing branch.
What if you wanted include all the changes made to the fencing branch on the master branch? We can easily accomplish this by merging the branch into master with:
```
git merge branch_name
```
In a moment, you'll merge branches. Keep in mind: Your goal is to update master with changes you made to fencing: fencing is the giver branch, since it provides the changes, master is the receiver branch, since it accepts those changes.

What would happen if you made a commit on master before you merged the two branches? Furthermore, what if the commit you made on master altered the same exact text you worked on in fencing? When you switch back to master and ask Git to merge the two branches, Git doesn't know which changes you want to keep. This is called a merge conflict.
Let's say you decide you'd like to merge the changes from fencing into master. Here's where the trouble begins! You've made commits on separate branches that alter the same line in conflicting ways. Now, when you try to merge fencing into master, Git will not know which version of the file to keep.

In Git, branches are usually a means to an end. You create them to work on a new project feature, but the end goal is to merge that feature into the master branch. After the branch has been integrated into master, it has served its purpose and can be deleted.
```
git branch -d branch_name
```
A remote is a shared Git repository that allows multiple collaborators to work on the same Git project from different locations. Collaborators work on the project independently, and merge changes together when they are ready to do so.

In order to get your own replica of a project, you'll need to clone it:
```
git clone remote_location clone_name
```
In this command, remote_location tells Git where to go to find the remote. This could be a web address, or a filepath, such as: /Users/teachers/Documents/some-remote. Clone_name is the name you give to the directory in which Git will clone the repository.
One thing that Git does behind the scenes when you clone remote_location is give the remote address the name origin, so that you can refer to it more conveniently.
You can see a list of a Git project's remotes with the command:
```
git remote –v
```
Notice the output:
```
origin    /home/ccuser/workspace/curriculum/science-quizzes (fetch)
origin    /home/ccuser/workspace/curriculum/science-quizzes (push)
```
-	Git lists the name of the remote, origin, as well as its location.
-	Git automatically names this remote origin, because it refers to the remote repository of origin. However, it is possible to safely change its name.
-	The remote is listed twice: once for (fetch) and once for (push). 
An easy way to see if changes have been made to the remote and bring the changes down to your local copy is with:
```
git fetch
```
This command will not merge changes from the remote into your local repository. It brings those changes onto what's called a remote branch.

Now we'll use the git merge command to integrate origin/master into your local master branch:
```
git merge origin/master
```
The workflow for Git collaborations typically follows this order:
-	Fetch and merge changes from the remote
-	Create a branch to work on a new project feature
-	Develop the feature on your branch and commit your work
-	Fetch and merge from the remote again (in case new commits were made while you were working)
-	Push your branch up to the remote for review

Steps 1 and 4 are a safeguard against merge conflicts, which occur when two branches contain file changes that cannot be merged with the git merge command. Step 5 involves git push, a command you will learn in the next exercise.
```
git push origin your_branch_name
```
will push your branch up to the remote, origin. From there, Sally can review your branch and merge your work into the master branch, making it part of the definitive project version.

#### GITHUB
Create a repository folder on GitHub. Give that new repository a name and get a URL to that new repository. Make an alias for that URL with this command:
```
git remote add myAlias theLongURLtoYourRepoOnGitHub
```
Push files to your repository on GitHub from your desktop:
```
git push –u myAlias master
```
The default command to push files from desktop to GitHub
```
git push origin master
```
Clone a project from a GitHub repo:
```
git clone theLongURLtoYourRepoOnGitHub
```
If you have an alias for the URL created, use that alias instead the URL link.

To clone the project in a particular directory add the name of the directory at the end
```
git clone theLongURLtoYourRepoOnGitHub theNameOfDirectory
```
If you made any changes on the origin (through GitHub site) and need to reflect the changes on your desktop repo, use the command:
```
git pull
```
To delete a branch on GitHub use:
```
git push origin --delete nameOfTheBranch
```

#### IGNORING FILES
To create a list of files you want to ignore create a new hidden file called ```.gitignore```:
```
touch .gitignore
```
Put files you want to be ignored by Git in this file. To get more info on the ```.gitignore``` file configuration:
```
git help gitignore
```
Add ```.gitignore``` file to the staging area:
```
git add .gitignore
```
Commit it:
```
git commit –m "Add .gitignore"
```
Push it to the GitHub:
```
git push
```
