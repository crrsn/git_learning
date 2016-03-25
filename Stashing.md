stash stæʃ (v)  = stash away утаивать, припрятывать, копить

### Saves modified files
```
$ git stash save
```
So, write now all changes are hidden.

### Bring stashed files back

```
$ git stash apply
```
Now we see the changes.

### You can have multiple stashes

```
$ git stash list
stash@{0}: WIP on master: 686b55d Add wolves.
stash@{1}: WIP on develop: b2bdead Add dogs.
...
```

WIP - work in progress

`stash@{0}` is the defualt when applying; specify the stash name to apply a different one:

```
$ git stash apply stash@{1}
```

### Drop stashes

`git stash drop` discards a stash

For example:

```
$ git stash list
stash@{0}: WIP on develop: b2bdead Add dogs.
```
Stash has been applied but it's still here.

```
$ git stash drop
Dropped (6dc716f...)
``` 
Delete it from list

```
$ git stash list
```

Old stash is gone.

### Shortcuts

``
git stash 
``
``
git stash save
``

``
git stash apply
``
``
git stash apply statsh@{0}
``

``
git stash drop
``
``
git stash drop stash@{0}
``

``
git stash pop
``
``
git stash appy +
git stash drop
``

### Stash conflicts

Conflicts are possible when applying a stash.
```
$ git stash apply
error: Your local changes to the following files would be overwritten by merge:
index.html
Please, commit your changes or stash them before you can merge.
Aborting
```

Commit or reset (`git reset --hard HEAD`) your local changes and then make 
```
$ git stash apply
# On branch develop
# Changes not staged for commit:
...
# modified: index.html
```
Success!

or
```
$ git stash apply
Auto-merging index.html
CONFLICT (content): Merge conflict in index.html
```
You need to merge the conflicted lines as usual...

If you're using the `pop` shortcut, and thers's a conflict
```
$ git stash pop
Auto-merging index.html
CONFLICT (content): Merge conflict in index.html
```
You _also_ need to merge the conflicted lines as usual...
And the stash won't be dropped automatically
```
$ git stash list
stash@{0}: WIP on develop: b2bdead Add dogs.
```
So be sure to do it manually
```
$ git stash drop
Dropped refs/stash@{0} (e4ba8a4...)
```
### Keep index

Suppose we have
```
$ git status
# On branch develop
# Changes to be commited:
#  new file: gerbil.html <-- we want to commit this
#
# Changes not staged for commit:
#
#  modified: index.html  <-- and stash everything else
```
```
$ git stash save
Saved working directory and index state...
```
```
$ git status
# On branch develop nothing to commit (working directory clean)
```
Whoops, everything is stashed.

Stashed staging areas get restored later:
```
$ git stash pop
# On branch develop
# Changes to be commited:
#
#  new file: gerbil.html
#
# Changes not staged for commit:
#
#  modified: index.html
#
Dropped refs/stash@{0} (de4105a...)
```
`**--keep-index**` option causes the staging area not to be stashed 
```
$ git stash save --keep-index
Saved working directory and index state
HEAD is now at b2bdead Add dogs.
```
```
$ git status
# On branch develop
# Changes to be commited:
#
#  new file:  gerbil.html
```
Now we can commit the changes:
```
$ git commit -m "Add gerbils section."
[gerbils 130a661] Add gerbils section.
1 file changed, 7 insertions(+)
create mode 100644 gerbil.html
```











