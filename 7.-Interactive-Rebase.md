What if we need to alter commits in the branch?
```
$ git rebase -i HEAD~3
```
`-i` - interactive mode
`HEAD~3` - commit to replay onto

Popups up an editor with the rebase script:
```
pick 9629e9b Add capybaras to index.            |
pick 21e37b1 Add capybaras page.                | This commands will execute when you close the editor
pick eb7d5a0 Actually, the plural is 'capybara'.|

# Rebase 4202447..eb7d5a0 onto 4202447
#
# Commands:
# p, pick = use commit
# r, reword = use commit, but edit the commit message
# e, edit = use commit, but stop for ammending
# s, squash = use commit, but meld into previous commit
# f, fixup = like "squash", but discard this commit's log message
# x, exec = run command (the rest of the line) using shell

```
We didn't make any changes... - the default script just replays the same commits.

Interactive rebase alters every commit **after** the one you specify:
```
$ git rebase -i HEAD <- there's no commits after HEAD!
```
### Reorder commits
```
$ git log --oneline
9afe987 Actually, the plural is 'capybara'.
1ee9572 Add capybaras page.               |We want to re-order 
74e6f3e Add capybaras to index.           |these two commits
```
```
$ git rebase -i HEAD~3
```
Editor (default script is in the original chronological order):
```
pick 1ee9572 Add capybaras to index. <- a
pick 74e6f3e Add capybaras page.     <- b             
pick 9afe987 Actually, the plural is 'capybara'.          
```
Swap the order, save, and close the editor 
```
pick 0511ab7 Add capybaras page.     <- b
pick 7d2edea Add capybaras to index. <- a           
pick 44d59fa Actually, the plural is 'capybara'.          
```
Commits get replayed in new order
```
$ git log --oneline
0511ab7 Actually, the plural is 'capybara'
7d2edea Add capybaras to index.
44d59fa Add capybaras page.
```
### Change messages
Change **pick** to **reword**, then save and exit
```
pick...
reword 9afe987 Actually, the plural is 'capybara'.
```
### Split commits
Change the **pick** to **edit**.
To split commits, we need to undo the changes that were just replayed:
```
$ git reset HEAD^ (HEAD^ - if we want to split the last commit)
Unstaged changes after reset:
M  capybara.html
M  index.html
```
since we don't specify **--hard**, files stay in working directory. Then commit them separately:
```
$ git add capybara.html
$ git commit -m "Change plural on detail page to 'capybara'"
```
```
$ git add index.html
$ git commit -m "Change plural on index page to 'capybara'"
```
New commits are in place, now we need to finish the rebase
```
$ git rebase --continue
```
```
$ git log --oneline
e8005f4 Change plural on index page to 'capybara'.
6e8e5d6 Change plural on detail page to 'capybara'.
7d2edea Add capybaras to index.
44d59fa Add capybaras page.
```
### Squash commits
**squash** merges a commit with the previous commit
```
...
pick 6e8e5d6 Change plural on detail page to 'capybara'
squash e80005f4 Change plural on index page to 'capybara' 
``` 
Another editor pops up, with the commits being squashed. Enter the message for the new commit, save, and exit.
```
$ git log --oneline
1c4614d Change plurals to 'capybara' <- one commit, with the changes to both files
7d2edea Add capybaras to index.
44d59fa Add capybaras page.
```