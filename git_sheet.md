Setup & Configuration
Initial Setup
Before using Git, configure your identity:

# Set your name and email globally
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Set default branch name to 'main'
git config --global init.defaultBranch main

# Set your preferred editor
git config --global core.editor "code --wait"  # VS Code
git config --global core.editor "vim"          # Vim
git config --global core.editor "nano"         # Nano
Viewing Configuration
# View all configurations
git config --list

# View specific configuration
git config user.name
git config user.email

# View configuration with location info
git config --list --show-origin
Configuration Levels
--system: System-wide configuration (all users)
--global: User-specific configuration
--local: Repository-specific configuration (default)
Repository Operations
Creating Repositories
# Initialize a new repository in current directory
git init

# Initialize with specific branch name
git init --initial-branch=main

# Clone an existing repository
git clone <repository-url>

# Clone to a specific directory
git clone <repository-url> <directory-name>

# Clone a specific branch
git clone -b <branch-name> <repository-url>

# Clone with limited history (shallow clone)
git clone --depth 1 <repository-url>
Repository Information
# Show remote repositories
git remote -v

# Show repository statistics
git count-objects -v

# Show repository size
du -sh .git/
Basic Workflow
Checking Status
# Check repository status (detailed)
git status

# Check status in short format
git status -s

# Check status and show ignored files
git status --ignored
Status indicators in short format:

?? - Untracked files
A - Added (staged)
M - Modified
D - Deleted
R - Renamed
C - Copied
Adding Files (Staging)
# Add specific file
git add <filename>

# Add multiple files
git add file1.txt file2.txt

# Add all files in current directory
git add .

# Add all files with specific extension
git add *.js

# Add files interactively
git add -i

# Add parts of a file (patch mode)
git add -p <filename>

# Add all tracked files (excluding untracked)
git add -u
Committing Changes
# Commit staged changes with message
git commit -m "Your commit message"

# Commit all tracked files (skip staging)
git commit -am "Your commit message"

# Commit with detailed message
git commit -m "Brief summary" -m "Detailed explanation"

# Commit and open editor for message
git commit

# Amend the last commit
git commit --amend

# Amend without changing message
git commit --amend --no-edit

# Commit with specific date
git commit --date="2023-12-25 10:00:00" -m "Christmas commit"
Branching & Merging
Branch Management
# List all local branches
git branch

# List all branches including remote
git branch -a

# List remote branches only
git branch -r

# Create new branch
git branch <branch-name>

# Create branch from specific commit
git branch <branch-name> <commit-hash>

# Create and switch to new branch
git checkout -b <branch-name>

# Switch to existing branch
git checkout <branch-name>

# Switch to previous branch
git checkout -

# Rename current branch
git branch -m <new-branch-name>

# Rename any branch
git branch -m <old-name> <new-name>

# Delete merged branch
git branch -d <branch-name>

# Force delete branch (even if not merged)
git branch -D <branch-name>

# Show branches with last commit
git branch -v
Merging Strategies
# Fast-forward merge (default when possible)
git merge <branch-name>

# Create merge commit even if fast-forward is possible
git merge --no-ff <branch-name>

# Squash merge (combine all commits into one)
git merge --squash <branch-name>

# Abort ongoing merge
git merge --abort

# Continue merge after resolving conflicts
git merge --continue
Handling Merge Conflicts
When conflicts occur:

Git marks conflicted files
Edit files to resolve conflicts
Remove conflict markers (<<<<<<<, =======, >>>>>>>)
Stage resolved files: git add <filename>
Complete merge: git commit
Remote Operations
Remote Repository Management
# List remote repositories
git remote -v

# Add remote repository
git remote add <remote-name> <repository-url>

# Remove remote
git remote remove <remote-name>

# Rename remote
git remote rename <old-name> <new-name>

# Change remote URL
git remote set-url <remote-name> <new-url>

# Show remote information
git remote show <remote-name>
Fetching and Pulling
# Fetch from default remote
git fetch

# Fetch from specific remote
git fetch <remote-name>

# Fetch all remotes
git fetch --all

# Fetch and prune deleted branches
git fetch --prune

# Pull changes (fetch + merge)
git pull

# Pull from specific remote and branch
git pull <remote-name> <branch-name>

# Pull with rebase instead of merge
git pull --rebase

# Pull and automatically stash/unstash changes
git pull --autostash
Pushing Changes
# Push to default remote and branch
git push

# Push to specific remote and branch
git push <remote-name> <branch-name>

# Push and set upstream tracking
git push -u <remote-name> <branch-name>

# Push all branches
git push --all

# Push tags
git push --tags

# Push specific tag
git push <remote-name> <tag-name>

# Force push (dangerous - rewrites history)
git push --force

# Safer force push (fails if remote has new commits)
git push --force-with-lease

# Delete remote branch
git push <remote-name> --delete <branch-name>
Viewing History
Basic Log Commands
# View commit history
git log

# Compact one-line format
git log --oneline

# Show graphical representation
git log --graph

# Combine graph with oneline
git log --graph --oneline --all

# Show file statistics
git log --stat

# Show actual changes
git log --patch

# Limit number of commits
git log -n 5
git log -5
Advanced Log Filtering
# Filter by author
git log --author="John Doe"

# Filter by date range
git log --since="2023-01-01"
git log --until="2023-12-31"
git log --since="2 weeks ago"

# Filter by commit message
git log --grep="bug fix"

# Filter by file
git log -- <filename>
git log --follow -- <filename>  # Follow renames

# Filter by content changes
git log -S "function_name"      # When function_name was added/removed
git log -G "regex_pattern"      # When pattern was added/removed
Comparing Changes
# Show unstaged changes
git diff

# Show staged changes
git diff --staged
git diff --cached

# Compare specific commits
git diff <commit1> <commit2>

# Compare branches
git diff <branch1> <branch2>

# Compare specific file between commits
git diff <commit1> <commit2> -- <filename>

# Show changes introduced by a commit
git show <commit-hash>

# Show file at specific commit
git show <commit>:<filename>
Undoing Changes
Working Directory Changes
# Discard changes in specific file
git checkout -- <filename>

# Discard all changes in working directory
git checkout -- .

# Restore file from specific commit
git checkout <commit> -- <filename>

# Using newer restore command (Git 2.23+)
git restore <filename>
git restore --staged <filename>  # Unstage
git restore --source=<commit> <filename>
Cleaning Untracked Files
# Remove untracked files
git clean -f

# Remove untracked files and directories
git clean -fd

# Preview what will be removed
git clean -n

# Interactive clean
git clean -i

# Remove ignored files too
git clean -fx
Staged Changes
# Unstage specific file
git reset HEAD <filename>

# Unstage all files
git reset HEAD

# Using newer restore command
git restore --staged <filename>
Commit History Changes
# Undo last commit, keep changes staged
git reset --soft HEAD~1

# Undo last commit, keep changes in working directory
git reset --mixed HEAD~1
git reset HEAD~1  # default is --mixed

# Undo last commit, discard all changes
git reset --hard HEAD~1

# Reset to specific commit
git reset --hard <commit-hash>

# Create new commit that undoes changes
git revert <commit-hash>

# Revert merge commit
git revert -m 1 <merge-commit-hash>
Stashing
Basic Stashing
# Stash current changes
git stash
git stash push  # newer syntax

# Stash with message
git stash save "Work in progress on feature X"
git stash push -m "Work in progress on feature X"

# Stash including untracked files
git stash -u
git stash --include-untracked

# Stash only specific files
git stash push <filename>
Managing Stashes
# List all stashes
git stash list

# Show stash content
git stash show
git stash show -p  # show patch

# Apply latest stash
git stash apply

# Apply specific stash
git stash apply stash@{2}

# Pop stash (apply and remove)
git stash pop
git stash pop stash@{1}

# Drop specific stash
git stash drop stash@{0}

# Clear all stashes
git stash clear
Advanced Stashing
# Create branch from stash
git stash branch <branch-name> stash@{0}

# Stash only staged changes
git stash --staged

# Interactive stashing
git stash -p
Tags
Creating Tags
# List all tags
git tag

# List tags matching pattern
git tag -l "v1.*"

# Create lightweight tag
git tag <tag-name>

# Create annotated tag
git tag -a <tag-name> -m "Tag message"

# Tag specific commit
git tag <tag-name> <commit-hash>

# Create signed tag
git tag -s <tag-name> -m "Signed tag"
Managing Tags
# Show tag information
git show <tag-name>

# Delete local tag
git tag -d <tag-name>

# Push specific tag
git push origin <tag-name>

# Push all tags
git push --tags

# Delete remote tag
git push origin --delete <tag-name>
git push origin :refs/tags/<tag-name>

# Checkout tag (creates detached HEAD)
git checkout <tag-name>

# Create branch from tag
git checkout -b <branch-name> <tag-name>
Advanced Operations
Rebasing
# Rebase current branch onto another
git rebase <base-branch>

# Interactive rebase (last 3 commits)
git rebase -i HEAD~3

# Continue rebase after resolving conflicts
git rebase --continue

# Skip current commit during rebase
git rebase --skip

# Abort rebase
git rebase --abort

# Rebase onto specific commit
git rebase --onto <new-base> <old-base> <branch>
Interactive rebase options:

pick - use commit as-is
reword - change commit message
edit - stop to amend commit
squash - combine with previous commit
fixup - like squash but discard message
drop - remove commit
Cherry-picking
# Apply specific commit to current branch
git cherry-pick <commit-hash>

# Cherry-pick without creating commit
git cherry-pick -n <commit-hash>

# Cherry-pick range of commits
git cherry-pick <start-commit>..<end-commit>

# Continue cherry-pick after resolving conflicts
git cherry-pick --continue

# Abort cherry-pick
git cherry-pick --abort
Searching and Debugging
# Search in commit messages
git log --grep="search term"

# Search in code across all commits
git log -S "search term" --source --all

# Search in current files
git grep "search term"

# Search in specific commit
git grep "search term" <commit-hash>

# Find when a bug was introduced (binary search)
git bisect start
git bisect bad <bad-commit>
git bisect good <good-commit>
# Test each commit Git suggests
git bisect good  # if commit is good
git bisect bad   # if commit is bad
git bisect reset # when done
Aliases
Create shortcuts for frequently used commands:

# Basic aliases
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit

# Advanced aliases
git config --global alias.lg "log --oneline --graph --all"
git config --global alias.unstage "reset HEAD --"
git config --global alias.last "log -1 HEAD"
git config --global alias.visual "!gitk"
Common Workflows
Feature Branch Workflow
# 1. Update main branch
git checkout main
git pull origin main

# 2. Create feature branch
git checkout -b feature/user-authentication

# 3. Work on feature
# ... make changes ...
git add .
git commit -m "Add login functionality"
git commit -m "Add password validation"

# 4. Push feature branch
git push -u origin feature/user-authentication

# 5. Create pull request (on GitHub/GitLab/etc.)

# 6. After approval, merge via web interface or:
git checkout main
git pull origin main
git merge feature/user-authentication

# 7. Clean up
git branch -d feature/user-authentication
git push origin --delete feature/user-authentication
Hotfix Workflow
# 1. Create hotfix branch from main
git checkout main
git pull origin main
git checkout -b hotfix/security-patch

# 2. Fix the critical issue
git add .
git commit -m "Fix security vulnerability in authentication"

# 3. Merge to main
git checkout main
git merge hotfix/security-patch

# 4. Tag the release
git tag -a v1.2.1 -m "Security hotfix v1.2.1"

# 5. Push changes
git push origin main
git push origin v1.2.1

# 6. Also merge to develop if using GitFlow
git checkout develop
git merge hotfix/security-patch
git push origin develop

# 7. Clean up
git branch -d hotfix/security-patch
Release Workflow
# 1. Create release branch
git checkout develop
git pull origin develop
git checkout -b release/v2.0.0

# 2. Finalize release (version bumps, changelog, etc.)
git add .
git commit -m "Prepare v2.0.0 release"

# 3. Merge to main
git checkout main
git merge release/v2.0.0

# 4. Tag release
git tag -a v2.0.0 -m "Release version 2.0.0"

# 5. Merge back to develop
git checkout develop
git merge release/v2.0.0

# 6. Push everything
git push origin main
git push origin develop
git push origin v2.0.0

# 7. Clean up
git branch -d release/v2.0.0
Best Practices
Commit Messages
Follow conventional commit format:

<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
Types:

feat: New feature
fix: Bug fix
docs: Documentation changes
style: Code style changes (formatting, etc.)
refactor: Code refactoring
test: Adding or updating tests
chore: Maintenance tasks
Examples:

feat(auth): add JWT token validation

fix: resolve memory leak in image processing

docs: update API documentation for v2.0

refactor(database): optimize query performance
Branch Naming Conventions
feature/feature-name
bugfix/issue-description
hotfix/critical-issue
release/version-number
General Guidelines
Commit Often: Make small, focused commits
Write Good Messages: Clear, descriptive commit messages
Use Branches: Separate features, bugs, and experiments
Keep History Clean: Use rebase for feature branches
Test Before Pushing: Ensure code works before sharing
Pull Before Push: Always sync with remote before pushing
Use .gitignore: Exclude unnecessary files
Back Up Important Work: Push branches to remote regularly
.gitignore Best Practices
Common patterns to ignore:

# Dependencies
node_modules/
vendor/

# Build outputs
dist/
build/
*.exe
*.dll

# IDE files
.vscode/
.idea/
*.swp

# OS files
.DS_Store
Thumbs.db

# Logs
*.log
logs/

# Environment files
.env
.env.local

# Temporary files
*.tmp
*.temp
Security Considerations
Never commit sensitive data (passwords, API keys, etc.)
Use environment variables for secrets
Review changes before committing
Use signed commits for important repositories
Regularly update Git and related tools
Be cautious with force push operations
