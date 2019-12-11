 **`git stash`**
Stashing is handy if you need to quickly switch context and work on something else, but you're mid-way through a code change and aren't quite ready to commit.

**to stash** - to save, to store something
> > guardar algo, esconder 
> 
_`EXPLANATION`_ Git takes your uncommited changes, both staged (changes added to the index through `git add`) and unstaged, saves them for later use and then reverts them from your working copy.

By default, running  `git stash`  will stash:

-   changes that have been added to your index (staged changes)
-   changes made to files that are currently tracked by Git (unstaged changes)
---
**`git stash pop`**

Popping your stash removes the changes from your stash and reapplies them to your working copy.

---
**`git stash apply`**
Reapplies the changes to your working copy _and_ keeps them in your stash.

_`INFO`_ This is useful if you want to apply the same stashed changes to multiple branches.

---

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQwNDc4MjgwOV19
-->