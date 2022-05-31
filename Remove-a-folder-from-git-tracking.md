**Step 1.** Add the folder path to your repo's root .gitignore file.

```
path_to_your_folder/
```

**Step 2.** Remove the folder from your local git tracking, but keep it on your disk.

```
git rm -r --cached path_to_your_folder/
```

**Step 3.** Push your changes to your git repo.

### References

https://stackoverflow.com/a/30360954/7848330