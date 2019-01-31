### Simple Way to remove untracked files

The simple way is to **add all** of them first **and reset** the repo as below

```
git add --all
git reset --hard HEAD
```

### To untrack only one file use
```
 git reset HEAD <file>
```

<img src="http://devcookbook.com/git/1.png" width=700>
<br>
<br>

```
$ git reset HEAD app/fabric.properties
```

<br>
<br>
<img src="http://devcookbook.com/git/2.png" width=700>

## Links

1. https://stackoverflow.com/a/37614185