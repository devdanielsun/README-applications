You can make a batch script and save it into your path.

1. Make a folder in ur userprofile named `bin`
2. Add `%USERPROFILE%\bin` to your PATH environment variable. Then save your scripts in there.
3. Make example.cmd
```bash
cd my/very/long/path/that/i/cannot/remember
```

4. Now you can type quickcd at the command line. It can also be called inside a script using the call function
`example`

---

#### List of git fetch prune:

`git-list-untracked.cmd`

```bash
git fetch --prune && git branch -r | awk "{print \$1}" | egrep -v -f /dev/fd/0 <(git branch -vv | grep origin) | awk "{print \$1}"
```

---

#### Execute git fetch prune:

`git-remove-untracked.cmd`

```bash
git fetch --prune && git branch -r | awk "{print \$1}" | egrep -v -f /dev/fd/0 <(git branch -vv | grep origin) | awk "{print \$1}" | xargs git branch -d
```
