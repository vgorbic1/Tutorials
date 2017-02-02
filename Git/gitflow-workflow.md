## Gitflow Workflow
- Create a repository on GitHub.
- Clone repository to local desktop. Go directly to the development folder. The cloned repository will be created in its own folder.  
```
git clone (insert ssh or http repository address)
```
###Creating a Release Branch
Let’s assign master branch to a release branch. 
- Create a codebase branch called develop branch locally.
```
git checkout -b develop
```
- Immediately create a develop branch remotely:  
```
git push -u origin develop
```

###Creating a Feature Branch
- Create a feature branch locally:
```
git checkout -b feature1
```
- Make changes to the code or add files locally.
- Add changes to the develop branch locally:
```
git add file.txt
```
- Commit changes locally:
```
git commit -m "Add file"
```
- Create and push all changes to feature branch remotely:
```
git push -u origin feature1
```

###Integrate Feature Branch with Develop Branch
- Checkout the develop branch locally:
```
git checkout develop
```
- Get all remote changes that may be done on develop branch:
```
git pull
```
- Integrate changes locally:
```
git merge feature1
```
- Merge changes remotely:
```
git push
```

###Integrate Develop Branch with Master Branch
- Checkout the master branch locally:
```
git checkout master
```
- Get all remote changes that may be done on master branch:
```
git pull
```
- Integrate changes locally:
```
git merge develop
```
- Merge changes remotely:
```
git push
```
- Tag the release locally:
```
git tag "1.0.0.RELEASE" -m "Add 1.0.0 release"
```
- Tag the release remotely:
```
git push --tag
```
![gitflow-workflow](https://cloud.githubusercontent.com/assets/13823751/22400340/a4c4c82e-e577-11e6-94f1-948791ca4df1.jpg)
