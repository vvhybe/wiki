```bash
# Create an orphan branch
git checkout --orphan branch

# clear any existing files
git rm -rf .

# Create empty commit
git commit --allow-empty -m "Initial empty commit"

# push to remote
gir push origin branch
```

