[link](https://stackoverflow.com/a/8981216)

If someone else pushed changes to the same branch, you probably want to avoid destroying those changes. The `--force-with-lease` option is the safest, because it will abort if there are any upstream changes:
```
git push --force-with-lease <repository> <branch>
```
Or you can use `--force`:
```
git push --force <repository> <branch>
```