# Comprehensive Guide to Using GitHub

GitHub is a powerful platform for version control and collaboration. This guide will walk you through everything from setting up your account to advanced collaboration techniques.

## Table of Contents
1. Getting Started with GitHub
2. Basic Git Commands
3. Working with Repositories
4. Understanding Branches
5. Pull Requests and Code Reviews
6. GitHub Issues and Project Management
7. GitHub Actions and CI/CD
8. Advanced GitHub Features

## Getting Started with GitHub

### 1. Create a GitHub Account
- Visit [github.com](https://github.com) and sign up for an account
- Choose a username, email, and password
- Verify your email address

### 2. Install Git
- **Mac**: 
  ```
  brew install git
  ```
- **Windows**: Download from [git-scm.com](https://git-scm.com)
- **Linux**: 
  ```
  sudo apt-get install git
  ```

### 3. Configure Git
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

### 4. Set Up SSH Keys (Recommended)
```bash
# Generate SSH key
ssh-keygen -t ed25519 -C "your.email@example.com"

# Start SSH agent
eval "$(ssh-agent -s)"

# Add SSH key to agent
ssh-add ~/.ssh/id_ed25519

# Copy public key to clipboard (Mac)
pbcopy < ~/.ssh/id_ed25519.pub
```
Then add the key to your GitHub account under Settings > SSH and GPG keys.

## Basic Git Commands

### Essential Commands
```bash
# Check Git status
git status

# Add files to staging
git add filename.txt    # Add specific file
git add .               # Add all files

# Commit changes
git commit -m "Descriptive commit message"

# Push changes to remote
git push origin main

# Pull changes from remote
git pull origin main

# View commit history
git log
```

### Example Workflow
```bash
# Create a new file
echo "# My Project" > README.md

# Check status
git status
# Output: Untracked files: README.md

# Add the file
git add README.md

# Commit the change
git commit -m "Add README file"

# Push to remote repository
git push origin main
```

## Working with Repositories

### Creating a New Repository
**On GitHub:**
1. Click the "+" icon in the upper right corner
2. Select "New repository"
3. Name your repository
4. Add a description (optional)
5. Choose public or private
6. Initialize with a README (optional)
7. Click "Create repository"

**From Command Line:**
```bash
# Create a new directory
mkdir my-project
cd my-project

# Initialize Git repository
git init

# Create a README file
echo "# My Project" > README.md

# Add and commit
git add README.md
git commit -m "Initial commit"

# Connect to GitHub repository
git remote add origin git@github.com:username/my-project.git

# Push to GitHub
git push -u origin main
```

### Cloning an Existing Repository
```bash
# Clone via HTTPS
git clone https://github.com/username/repository.git

# Clone via SSH (recommended if you have SSH set up)
git clone git@github.com:username/repository.git

# Clone to a specific folder
git clone git@github.com:username/repository.git my-folder
```

### Example: Cloning and Making Changes
```bash
# Clone repository
git clone git@github.com:username/project.git
cd project

# Make changes
echo "New content" >> README.md

# Check what changed
git diff

# Stage and commit
git add README.md
git commit -m "Update README with new content"

# Push changes
git push origin main
```

## Understanding Branches

Branches allow you to develop features, fix bugs, or experiment with new ideas in isolation from your main codebase.

### Basic Branch Commands
```bash
# List all branches
git branch

# Create a new branch
git branch feature-name

# Switch to a branch
git checkout feature-name

# Create and switch in one command
git checkout -b feature-name

# Push branch to remote
git push -u origin feature-name

# Delete a branch locally
git branch -d feature-name

# Delete a branch remotely
git push origin --delete feature-name
```

### Example: Feature Branch Workflow
```bash
# Create and switch to a feature branch
git checkout -b add-login-feature

# Make changes
touch login.js
echo "function login() { /* code */ }" > login.js

# Stage and commit
git add login.js
git commit -m "Add login functionality"

# Push to remote
git push -u origin add-login-feature

# Later, merge back to main (after PR approval)
git checkout main
git pull origin main
git merge add-login-feature
git push origin main
```

### Example: Working with Multiple Branches
```bash
# Create multiple feature branches
git checkout -b feature-1
# Make changes, commit
git add .
git commit -m "Implement feature 1"
git push -u origin feature-1

# Switch to another branch
git checkout main
git checkout -b feature-2
# Make changes, commit
git add .
git commit -m "Implement feature 2"
git push -u origin feature-2

# Switch back to main
git checkout main
```

### Example: Resolving Merge Conflicts
```bash
# Try to merge a branch
git checkout main
git merge feature-branch

# If conflicts occur, edit the files to resolve conflicts
# Files will contain markers like:
# <<<<<<< HEAD
# current content
# =======
# incoming content
# >>>>>>> feature-branch

# After resolving, stage the files
git add .

# Complete the merge
git commit -m "Merge feature-branch, resolve conflicts"
```

## Pull Requests and Code Reviews

### Creating a Pull Request
1. Push your branch to GitHub:
   ```bash
   git push -u origin feature-branch
   ```
2. Go to the repository on GitHub
3. Click "Compare & pull request"
4. Add a title and description
5. Select reviewers (optional)
6. Click "Create pull request"

### Example: Complete PR Workflow
1. **Create a branch for your feature**
   ```bash
   git checkout -b add-user-profile
   ```

2. **Make changes and commit**
   ```bash
   # Create new files
   touch user-profile.js user-profile.css

   # Edit files with your code
   # ...

   # Stage and commit
   git add user-profile.js user-profile.css
   git commit -m "Add user profile component"
   ```

3. **Push branch to GitHub**
   ```bash
   git push -u origin add-user-profile
   ```

4. **Create PR on GitHub**
   - Go to repository
   - Click "Compare & pull request"
   - Add title: "Add user profile component"
   - Description: "This PR adds a new user profile component with the following features:
     - Profile picture upload
     - Bio editor
     - Social links section"
   - Request reviews from team members
   - Click "Create pull request"

5. **Address review comments**
   ```bash
   # Make requested changes
   # Commit changes
   git add .
   git commit -m "Address review feedback"
   git push origin add-user-profile
   ```

6. **Merge PR**
   - Once approved, click "Merge pull request" on GitHub
   - Choose merge method (merge, squash, or rebase)
   - Click "Confirm merge"
   - Delete branch when prompted

7. **Update local main**
   ```bash
   git checkout main
   git pull origin main
   ```

## GitHub Issues and Project Management

### Creating and Managing Issues
1. Go to the "Issues" tab in your repository
2. Click "New issue"
3. Add a title and description
4. Assign labels, projects, and milestones
5. Assign to team members

### Example: Issue Workflow
1. **Create an issue**
   - Title: "Fix navigation bar on mobile devices"
   - Description: "The navigation bar doesn't collapse properly on mobile screens smaller than 320px. This needs to be fixed to improve mobile usability."
   - Labels: "bug", "mobile", "UI"
   - Assign to: [team member]

2. **Reference issue in commits**
   ```bash
   git checkout -b fix-mobile-nav
   # Make changes
   git commit -m "Fix mobile navigation collapse #42"
   ```

3. **Close issue with PR**
   - In PR description: "Fixes #42"
   - When the PR is merged, the issue will automatically close

### Using Project Boards
1. Go to the "Projects" tab
2. Create a new project
3. Add columns (e.g., To Do, In Progress, Review, Done)
4. Add issues to the board
5. Move issues between columns as work progresses

## GitHub Actions and CI/CD

### Setting Up a Basic GitHub Action
1. Create a `.github/workflows` directory in your repository
2. Add a YAML file, e.g., `ci.yml`:

```yaml
name: CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v2
    
    - name: Set up Node.js
      uses: actions/setup-node@v2
      with:
        node-version: '14'
        
    - name: Install dependencies
      run: npm ci
      
    - name: Run tests
      run: npm test
```

### Example: Automated Deployment Workflow
```yaml
name: Deploy to Production

on:
  push:
    branches: [ main ]

jobs:
  deploy:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v2
    
    - name: Set up Node.js
      uses: actions/setup-node@v2
      with:
        node-version: '14'
        
    - name: Install dependencies
      run: npm ci
      
    - name: Build
      run: npm run build
      
    - name: Deploy to server
      uses: easingthemes/ssh-deploy@v2
      env:
        SSH_PRIVATE_KEY: ${{ secrets.SERVER_SSH_KEY }}
        ARGS: "-rltgoDzvO"
        SOURCE: "dist/"
        REMOTE_HOST: ${{ secrets.REMOTE_HOST }}
        REMOTE_USER: ${{ secrets.REMOTE_USER }}
        TARGET: ${{ secrets.REMOTE_TARGET }}
```

## Advanced GitHub Features

### Git Rebase
```bash
# Rebase feature branch onto latest main
git checkout feature-branch
git rebase main

# Interactive rebase to clean up commits
git rebase -i HEAD~3  # Rebase last 3 commits
```

### Git Stash
```bash
# Save changes without committing
git stash

# List stashes
git stash list

# Apply most recent stash
git stash apply

# Apply specific stash
git stash apply stash@{2}

# Remove most recent stash
git stash drop

# Apply and remove most recent stash
git stash pop
```

### GitHub Gists
1. Go to [gist.github.com](https://gist.github.com)
2. Create public or secret gists for code snippets
3. Share and embed gists in documentation

### GitHub Pages
1. Go to repository settings
2. Scroll to "GitHub Pages" section
3. Select source branch (main or gh-pages)
4. Choose folder (root or /docs)
5. Save to publish your site at `https://username.github.io/repository`

### Example: Setting Up GitHub Pages
```bash
# Create a gh-pages branch
git checkout -b gh-pages

# Add website files
echo "<html><body><h1>My Project Site</h1></body></html>" > index.html

# Push to GitHub
git add index.html
git commit -m "Add GitHub Pages site"
git push -u origin gh-pages
```

## Best Practices

1. **Write meaningful commit messages**
   - Bad: "Fix stuff"
   - Good: "Fix navigation dropdown not closing on mobile devices"

2. **Commit often, push regularly**
   - Make small, focused commits
   - Push to remote to back up your work

3. **Use branches for features and fixes**
   - Never work directly on main
   - Create descriptive branch names (e.g., `feature/user-authentication`, `fix/login-error`)

4. **Keep your local repo updated**
   ```bash
   git checkout main
   git pull origin main
   ```

5. **Review your changes before committing**
   ```bash
   git diff
   git add --patch  # Interactive staging
   ```

6. **Use .gitignore for files that shouldn't be tracked**
   ```
   # Example .gitignore
   node_modules/
   .env
   .DS_Store
   *.log
   ```

This guide covers the essentials of GitHub, but there's always more to learn. GitHub's documentation is excellent for further reading on specific topics.
