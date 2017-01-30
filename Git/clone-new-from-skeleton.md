## Clone a Completely New Repository Using an Existing Remote Skeleton Repository
Clone the remote Skeleton Repository to your local machine and give it a new (different) name:
```
git clone https://github.com/username/skeleton.git myapp
```
Get inside the new repository folder.
```
cd myapp
```
Remove all links to the skeleton repository:
```
git remote rm origin
```
Create a new repository on GitHub, say "myapp".

Ceate a new link between your new local repository and new remote repository:
```
git remote add origin https://github.com/username/myapp.git
```
Push up all files from your new local repo to the new remote repo fot the first time:
```
git push -u origin --all
```
