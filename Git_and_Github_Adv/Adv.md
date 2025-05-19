## **Topics Covered**  
1. Pull Requests – Collaborating in teams.  
2. Reset & Revert – Undo changes safely.  
3. Stashing – Saving work temporarily.  
4. Cherry-picking – Selecting specific commits.  
5. Rebasing – Maintaining a clean history.  
6. Branching Strategies – Industry best practices.  


## Commands

1. Soft Reset (keeps changes staged).  
   ```bash
   git reset --soft HEAD~1
   ```  
2. Mixed Reset (unstages changes but keeps files).  
   ```bash
   git reset --mixed HEAD~1
   ```  
3. Hard Reset (removes all changes).  
   ```bash
   git reset --hard HEAD~1
   ```  
4. Revert a commit safely.  
   ```bash
   git revert HEAD

## git reset 

- What it does:Moves the HEAD (and optionally the current branch pointer) to a previous commit.
               Can change your working directory, staging area (index), or both, depending on the option used.

- When to use:Local undo of commits before pushing.
              Rewriting history when you want a clean commit history (e.g., squashing, removing bad commits).

Unstaging files (git reset <file>).

Example:
```bash
git reset --hard HEAD~1  # Deletes the latest commit and resets working directory
```
⚠️ Avoid using reset on public/shared branches—it rewrites history

## git revert

- What it does:Creates a new commit that undoes the changes from a previous commit.
               Safe for shared/public branches because it preserves history.

- When to use: Undo a commit that has already been pushed to a shared repo.
               Need a non-destructive way to reverse changes

## git stash

1. Modify a file without committing.  
   ```bash
   echo "Temporary Change" >> temp.txt
   git add temp.txt
   ```  
2. Stash the changes.  
   ```bash
   git stash
   ```  
3. Switch to another branch and apply the stash.  
   ```bash
   git checkout main
   git stash pop

- When to Use: git stash when you want to temporarily save your uncommitted changes (modified or staged files) without committing them, so you can work on something else (like switching branches or pulling latest code).


## git stash apply vs git stash pop

- git stash apply: Reapplies stashed changes to your working directory.
                   Does NOT remove the stash from the stash list.
                   Useful when you want to reuse or keep the stash for later.
                   Safer if you're unsure or want a backup.

- git stash pop: Reapplies stashed changes to your working directory.
                 Removes the stash from the stash list after applying.
                 Use when you're done with the stash and don't need it again.
                 Riskier if there's a conflict — stash could be lost.   

## git cherry-pick

1. Find the commit to cherry-pick.
   ```bash
   git log --oneline
   ```
2. Apply a specific commit to the current branch.
   ```bash
   git cherry-pick <commit-hash>
   ```
3. Resolve conflicts if any.
   ```bash
   git cherry-pick --continue
   ```

## How Cherry-Picking is Used in Bug Fixes
Cherry-picking allows you to apply a specific commit (or set of commits) from one branch to another — usually without merging the entire branch.

In bug fixing, it’s commonly used to:Backport fixes from the main branch to older release branches.
                                     Apply urgent fixes from a feature or hotfix branch to production without waiting for full integration.


## Risks of Cherry-Picking
- Duplicate commits: The same changes may exist in multiple branches with different hashes, making history harder to follow.

- Merge conflicts: Applying a commit out of its original context can lead to conflicts, especially if dependencies have changed.

- Loss of context: The cherry-picked commit might rely on earlier commits not included, leading to bugs or inconsistent behavior.

- History confusion: Repeated cherry-picks across branches can clutter logs and make it harder to trace changes.

## git rebase
 1. Fetch the latest changes.  
   ```bash
   git fetch origin main
   ```  
2. Rebase the feature branch onto main.  
   ```bash
   git rebase origin/main
   ```  
3. Resolve conflicts and continue.  
   ```bash
   git rebase --continue

## git merge vs git rebase:

- git merge: Combines two branches with a merge commit
             Does not change existing commit history
             Keeps a non-linear (branching) history
             Safe for shared/public branches
             Easier for teams to collaborate without rewriting history
             History can become cluttered with many merge commits

- git rebase: Moves your branch’s commits on top of another branch
              Rewrites history (changes commit hashes)
              Creates a linear, clean commit history
              Ideal for local or personal branches before merging
              Should not be used on shared branches after pushing
              Can simplify git log and git blame

## Best practices for rebasing

- Never rebase shared/public branches: Only rebase local/private branches to avoid breaking others' history.

- Create a backup branch before rebasing: Use git branch backup/your-branch as a safety net.

- Use interactive rebase (git rebase -i): To squash, reword, or drop commits for a cleaner history.

- Handle conflicts carefully: Fix files, run git add, then continue with git rebase --continue.

- Squash small or WIP commits: Combine multiple commits into one logical unit to simplify the history.

- Rebase onto latest main before merging: Keeps your branch up-to-date and avoids unnecessary merge commits.

- Use git log and git reflog for recovery: Use git reflog to recover lost commits if something goes wrong.

🚫 Avoid rebasing after pushing to remote
– Unless you’re the only one working on that branch.

# Branching Strategies Used in Companies

| Workflow            | Best For                        | Branches Used                                           | Key Benefit                         |
| ------------------- | ------------------------------- | ------------------------------------------------------- | ----------------------------------- |
| **Git Flow**        | Structured, versioned releases  | `main`, `develop`, `feature/*`, `release/*`, `hotfix/*` | Organized release process           |
| **GitHub Flow**     | Fast-moving teams, CI/CD        | `main`, `feature/*`                                     | Simplicity + continuous delivery    |
| **Trunk-Based Dev** | High-speed CI/CD & DevOps teams | `main` (or `trunk`), short-lived branches               | Frequent integration, fast releases |


# Which strategy is best for DevOps and CI/CD.

 ## Trunk-Based Development
- Fast integration: Developers push small, frequent changes directly to the main branch or short-lived branches.

- Simple branching: Minimal branches (usually just main or trunk), avoiding complex merges and delays.

- Enables automation: Works perfectly with CI/CD pipelines for build, test, and deployment.

- Supports feature flags: Incomplete features can be hidden from users while code is still deployed.

- Reduces merge conflicts: Frequent integration means fewer long-lived branches and fewer conflicts.


# Pros and cons of different workflows.

## Git Flow
✅ Pros
- Clear separation of concerns (features, releases, hotfixes)

- Good for large teams and structured release cycles

- Supports multiple versions in parallel (e.g., hotfix for v1 while developing v2)

❌ Cons
- Complex branching model (develop, feature, release, hotfix)

- Slower integration and deployment

- Not ideal for CI/CD or fast iteration

- - Merge conflicts are more likely due to long-lived branches

## GitHub Flow
✅ Pros
- Simple and lightweight

- Encourages continuous delivery and deployment

- Integrates well with pull requests and automated testing

- Good for small-to-medium teams or startups

❌ Cons
- No formal release or hotfix process

- Lacks structure for long-running development

- Assumes main is always stable and deployable, which requires discipline

## Trunk-Based Development
✅ Pros
- Fast integration, ideal for DevOps and CI/CD

- Encourages frequent, small commits

- Reduces merge conflicts by avoiding long-lived branches

- Easier to automate and maintain

❌ Cons
- Requires mature tooling (feature flags, test automation)

- Developers need discipline and solid test coverage

- Not ideal for teams unfamiliar with continuous delivery practices
  



