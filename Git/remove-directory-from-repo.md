## Remove directory from remote repository after adding it to .gitignore
If you committed and pushed some directory to github and after that, you altered the `.gitignore` file adding a directory that should
be ignored, you can remove (now ignored) directory from GitHub.
```
git rm -r --cached some-directory
git commit -m 'Remove the now ignored directory "some-directory"'
git push origin master
```
