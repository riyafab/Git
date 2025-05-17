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


