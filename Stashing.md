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
`--keep-index` **option causes the staging area not to be stashed** 
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
**Unstaged changes get stashed and restored as usual**
```
$ git stash pop
# On branch develop
# Changes not staged for commit:
#
#  modified:  index.html
#
no changes added to commit
Dropped refs/stash@{0} (db990c0...)
```
### Include untracked 
Normally, only **tracked** files get stashed

`--include-untracked` **option causes untracked files to be stashed, too**
```
$ git stash save --include-untracked
```
When stash is restored, untracked files will be, too:
```
$ git stash pop
# On branch develop
# Changes not staged for commit:
#
#  modified:  index.html
#
# Untracked files:
#
#  gerbil.html
```
### List options
`git stash list` can take any option `git log` can. For example: `--stat` **summarizes file changes**
```
$ git stash list --stat
stash@{0}: WIP on develop: b2bdead Add dogs.
gerbil.html  |  5 +++++
index.html   |  1 +
wolf.html    |  5 -----
3 files changed, ...
```
### Stash show
Shows one perticular stash:
```
$ git stash show stash@{0}
gerbil.html  |  5 +++++
index.html   |  1 +
2 files changed, 8 insertions(+)
```
Like **apply** and **drop**, acts on most recent stash by default:
```
$ git stash show 
gerbil.html  |  5 +++++
index.html   |  1 +
2 files changed, 8 insertions(+)
```
Also take any option `git log` can. For example, `--patch` **shows file diffs**
```
$ git stash show --patch
diff --git a/gerbil.html b/gerbil.html
+<!DOCTYPE html>
...
```
### Stash messages
You can provide a stash message when saving
```
$ git stash save "Add gerbils page, start index."
Saved working directory and index state
HEAD is now at b2bdead Add dogs.
```
```
$ git stash list
stash@{0}: On develop: Add gerbils page, start index.
stash@{1}: WIP on develop: b2bdead Add dogs.
...
```
### Branching
`git stash branch` checks a new branch out automatically...

and drops the stash automatically

```
$ git stash branch new_branch_name stash@{0}
Switched to a new branch 'new_branch_name'
# On branch new_branch_name
# Changes not staged for commit:
#
#  modified:  gerbil.html
#
Dropped stash@{0} (5797b65...)
```
New branch is an ordinary branch, ready for commits.
