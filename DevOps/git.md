
# Git Cheat Sheet

## Basic Configuration

- **Set username**: 
  ```bash
  git config --global user.name "Your Name"
  ```
- **Set email address**: 
  ```bash
  git config --global user.email "your_email@example.com"
  ```

## Creating Repositories

- **Initialize a new repository**: 
  ```bash
  git init
  ```
- **Clone an existing repository**: 
  ```bash
  git clone <repository-url>
  ```

## Basic Git Workflow

- **Check status**: 
  ```bash
  git status
  ```
- **Add files to staging area**: 
  ```bash
  git add <file-or-directory>
  git add .  # Add all changes
  ```
- **Commit changes**: 
  ```bash
  git commit -m "Commit message"
  ```
- **Pull latest changes from remote**: 
  ```bash
  git pull
  ```
- **Push local commits to remote repository**: 
  ```bash
  git push
  ```

## Branching

- **List branches**: 
  ```bash
  git branch
  ```
- **Create a new branch**: 
  ```bash
  git branch <branch-name>
  ```
- **Switch to a branch**: 
  ```bash
  git checkout <branch-name>
  ```
- **Create and switch to a new branch**: 
  ```bash
  git checkout -b <branch-name>
  ```
- **Delete a branch**: 
  ```bash
  git branch -d <branch-name>
  ```
- **Merge a branch into the current branch**: 
  ```bash
  git merge <branch-name>
  ```

## Viewing Changes

- **View changes**: 
  ```bash
  git diff
  ```
- **View log of commits**: 
  ```bash
  git log
  ```
- **View a specific commit**: 
  ```bash
  git show <commit-hash>
  ```

## Undoing Changes

- **Undo changes in a specific file**: 
  ```bash
  git checkout -- <file>
  ```
- **Revert a commit (create a new commit with undo changes)**: 
  ```bash
  git revert <commit-hash>
  ```
- **Reset to a specific commit (discard commits)**: 
  ```bash
  git reset --hard <commit-hash>
  ```

## Advanced Git

- **Stashing changes**:
  - Stash changes: `git stash`
  - Apply stashed changes: `git stash pop`
- **Interactive rebase**: 
  ```bash
  git rebase -i <commit-hash>
  ```
- **Squash commits**: Done during interactive rebase.
- **Cherry-pick a commit**: 
  ```bash
  git cherry-pick <commit-hash>
  ```

## Working with Remotes

- **View remote repositories**: 
  ```bash
  git remote -v
  ```
- **Add a remote repository**: 
  ```bash
  git remote add <remote-name> <remote-url>
  ```
- **Remove a remote repository**: 
  ```bash
  git remote remove <remote-name>
  ```

## Tags

- **Create a tag**: 
  ```bash
  git tag <tag-name> <commit-hash>
  ```
- **List tags**: 
  ```bash
  git tag
  ```
- **Delete a tag**: 
  ```bash
  git tag -d <tag-name>
  ```
- **Push tags to remote**: 
  ```bash
  git push --tags
  ```

## Gitignore

- **Ignoring files**: Create a `.gitignore` file in your project root and list files/folders to ignore.

## Tips and Tricks

- **Save credentials**: 
  ```bash
  git config --global credential.helper cache
  ```
- **Alias commands**: Set short aliases for commonly used commands in the `.gitconfig` file.

## Troubleshooting

- **Undo last commit but keep changes**: 
  ```bash
  git reset --soft HEAD~1
  ```
- **Resolve merge conflicts**: Manually edit the conflicted files, then add and commit them.



