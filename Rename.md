
- Initialize a new Git repository
```bash
git init
```

# Add files to staging area
```bash
git add .
```

# Commit changes
```bash
git commit -m "Your commit message"
```

# View commit history
```bash
git log
```

# View commit history in one line per commit
```bash
git log --oneline
```

# Pretty format for log (customize as needed)
```bash
git log --oneline --pretty=format:"%h - %an, %ar : %s"
```

# Push changes to remote origin
```bash
git push origin main
```

# Pull changes from remote origin
```bash
git pull origin main
```

# Clone a repository
```bash
git clone https://github.com/<your-username>/<repo-name>.git
```

# Fetch updates from remote
```bash
git fetch origin
```

# Create and switch to a new branch
```bash
git checkout -b branch_name
```

# List all branches
```bash
git branch
```

# Add a new remote
```bash
git remote add origin https://github.com/<your-username>/<repo-name>.git
```

# View configured remotes
```bash
git remote -v
```

# Set global email config
```bash
git config --global user.email "your-email@example.com"
```

# Set global username config
```bash
git config --global user.name "Your Name"
```

# Cherry-pick a specific commit using its hash
```bash
git cherry-pick <commit-hash>
```

# Add remote origin using a Personal Access Token (PAT)
git remote add origin https://<your-username>:<your-PAT>@github.com/<your-username>/90DaysOfDevOps.git

# Update existing remote origin URL
git remote set-url origin https://<your-username>:<your-PAT>@github.com/<your-username>/90DaysOfDevOps.git
