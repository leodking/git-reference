A guide to what the various forms of `git add` do:

Taken from this SO answer: https://stackoverflow.com/a/26039014/1907765

### Git Version 1.x

| Command | New Files | Modified Files | Deleted Files | Description |
|-|-|-|-|-|
| `git add -A` | ✔️ | ✔️ | ✔️ | Stage all (new, modified, deleted) files |
| `git add .` | ✔️ | ✔️ | ❌ | Stage new and modified files only in current folder |
| `git add -u` | ❌ | ✔️ | ✔️ | Stage modified and deleted files only |

### Git Version 2.x

| Command | New Files | Modified Files | Deleted Files | Description |
|-|-|-|-|-|
| `git add -A` | ✔️ | ✔️ | ✔️ | Stage all (new, modified, deleted) files |
| `git add .` | ✔️ | ✔️ | ✔️ | Stage all (new, modified, deleted) files in current folder |
| `git add --ignore-removal .` | ✔️ | ✔️ | ❌ | Stage new and modified files only |
| `git add -u` | ❌ | ✔️ | ✔️ | Stage modified and deleted files only |

### Long-form flags:

* `git add -A` is equivalent to `git add --all`
* `git add -u` is equivalent to `git add --update`
