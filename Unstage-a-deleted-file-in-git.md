Assuming you're wanting to undo the effects of `git rm <file>` or `rm <file>` followed by `git add -A` or something similar:

```
# this restores the file status in the index
git reset -- <file>
# then check out a copy from the index
git checkout -- <file>
```
To undo `git add <file>`, the first line above suffices, assuming you haven't committed yet.


https://stackoverflow.com/a/9591612/7848330