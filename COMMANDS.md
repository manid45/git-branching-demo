# Git Branching and Merging - Commands

## 1. Initialize
git init -b main
git config user.name "Your Name"
git config user.email "you@example.com"
git add .
git commit -m "Initial commit: add index.html and style.css"

## 2. feature-header branch
git switch -c feature-header
# In index.html, add right after <body>:
#   <header>
#     <h1>My Website</h1>
#   </header>
git add index.html
git commit -m "Add header"
git switch main
git merge feature-header
git log --oneline

## 3. Create the conflict (change the SAME line in both branches)
git switch -c branch-a
# Change the tagline line to: <p class="tagline">Welcome to Branch A</p>
git add index.html
git commit -m "Change tagline in branch-a"

git switch main
git switch -c branch-b
# Change the same line to: <p class="tagline">Hello from Branch B</p>
git add index.html
git commit -m "Change tagline in branch-b"

## 4. Merge and get the conflict
git switch main
git merge branch-a
git merge branch-b        # CONFLICT
git status

## 5. Resolve
# Edit index.html, remove <<<<<<<, =======, >>>>>>> lines, keep final text, e.g.:
#   <p class="tagline">Welcome to my website - Hello from Branch B</p>
git add index.html
git commit -m "Resolve merge conflict between branch-a and branch-b"
git log --oneline --graph --all

## 6. Cleanup (optional)
git branch -d feature-header branch-a branch-b
