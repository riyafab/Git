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
