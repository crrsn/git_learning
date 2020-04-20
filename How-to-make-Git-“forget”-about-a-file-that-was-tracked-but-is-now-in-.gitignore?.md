To stop tracking a file you need to remove it from the index:
```
git rm --cached <file>
```
If you want to remove a whole folder, you need to remove all files in it recursively.
```
git rm -r --cached <folder>
```
https://stackoverflow.com/a/1274447/7848330

It worked for me:
1. `git rm --cached <file>`
2. `git reset HEAD <file>...` to unstage
3. `git checkout -- <file>...` to discard changes in working directory