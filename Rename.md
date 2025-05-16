
# Initialize a new Git repository
```bash
git init
```

# Add files to staging area
git add .

# Commit changes
git commit -m "Your commit message"

# View commit history
git log

# View commit history in one line per commit
git log --oneline

# Pretty format for log (customize as needed)
git log --oneline --pretty=format:"%h - %an, %ar : %s"

# Push changes to remote origin
git push origin main

# Pull changes from remote origin
git pull origin main

# Clone a repository
git clone https://github.com/<your-username>/<repo-name>.git

# Fetch updates from remote
git fetch origin

# Create and switch to a new branch
git checkout -b branch_name

# List all branches
git branch

# Add a new remote
git remote add origin https://github.com/<your-username>/<repo-name>.git

# View configured remotes
git remote -v

# Set global email config
git config --global user.email "your-email@example.com"

# Set global username config
git config --global user.name "Your Name"

# Cherry-pick a specific commit using its hash
git cherry-pick <commit-hash>

# Add remote origin using a Personal Access Token (PAT)
git remote add origin https://<your-username>:<your-PAT>@github.com/<your-username>/90DaysOfDevOps.git

# Update existing remote origin URL
git remote set-url origin https://<your-username>:<your-PAT>@github.com/<your-username>/90DaysOfDevOps.git
