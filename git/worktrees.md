# Git Worktrees

* Git Worktrees are a simple way to work with multiple branches.
* Normally you have to switch between branches with `git branch blabla`.
* With worktrees you actually have a branch available as a folder:

![image](https://user-images.githubusercontent.com/6579452/206759611-8aca429a-67d7-4c9c-95d2-abda08a5a3c4.png)

* Here the branches are represented as a folder, in this example as `main`, `anothertestbranch` and `testbranch`.
* It's easy now to navigate as you only have to go into the folder, and there you can see the actual content of that branch.
* Git operations work the same, just go into the folder and execute your regular git commands like `git commit -m 'fix: something'`, `git push`

The trick behind this is that you have to git clone with a special parameter `--bare`, like this:

```shell
git clone --bare https://github.com/rdtechie/test-gh-actions test-gh-actions
```

Which means this: clone the bare repository into a folder called `test-gh-actions`
