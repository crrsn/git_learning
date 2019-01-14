1. Clone main project with `https`.
2. Open hidden file `.gitmodules` and change `url` from `git@github.com:` to `https`.
3. Then 
```
git submodule sync
git submodule update --init NAME_OF_SUBMODULE
```