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
