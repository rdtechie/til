# Git Contributors

To see who/what contributed onto a git repository, use the following:

```
git log --pretty=format:'%an%x09' main | sort | uniq
```

This will give a list of contributors sorted by name.
You can target a different branch by replacing `main` by the branch name.

