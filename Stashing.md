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