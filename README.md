# Learning Path Repository - Traders@SMU Alpha Program

Welcome to your learning journey! This repository is structured to guide you through a progressive learning path with organized materials, exercises, and projects.

## Welcome

This repository serves as your central hub for all course materials. Each level is broken down into weekly modules, allowing you to progress at a steady pace while building on previous knowledge.

## Repository Structure

This repository contains materials organized by levels (L1, L2) and weeks, along with a final project.

## Structure

- **L1**: Level 1 materials (Junior)
  - Week1 through Week8
- **L2**: Level 2 materials (Associate)
  - Week1 through Week8
- **Final_Project**: Final project materials

## Getting Started (Easy Setup Guide)

### Step 1: One-Time Setup (Do this first!)

1. **Install GitHub Desktop**
   - Go to [GitHub Desktop Download Page](https://desktop.github.com/)
   - Download and install GitHub Desktop for your computer
   - If you don't have a GitHub account, create one at [GitHub.com](https://github.com)
   - Open GitHub Desktop and sign in with your GitHub account

2. **Get Access to Traders@SMU**
   - Email your instructor with:
     - Your full name
     - Your GitHub username
     - Your program level (L1 or L2)
   - Wait for confirmation email that you've been added to the organization

### Step 2: Create Your Repository

1. **Create from Template**
   - Go to the [Traders@SMU student-template](https://github.com/Traders-SMU/student-template)
   - Click the green "Use this template" button
   - Select "Create a new repository"
   - For repository name, use this format exactly: `traders-smu-LEVEL-FULLNAME`
     - Example: If you're John Smith in L1: `traders-smu-L1-john-smith`
     - Example: If you're Jane Doe in L2: `traders-smu-L2-jane-doe`
   - Choose "Private" for repository visibility
   - Click "Create repository from template"

### Step 3: Set Up Local Copy

1. **Clone with GitHub Desktop**
   - Open GitHub Desktop
   - Click "File" → "Clone repository"
   - Find your new repository in the list
   - Choose where to save it on your computer
     - Remember this location! You'll need it later
   - Click "Clone"

### Step 4: Set Up Automatic Sync (One-Time Setup)

1. **Get Your Access Tokens** (Important! 🔑)
   
   You need two special passwords (tokens) to set up syncing. Let's get them one at a time:

   a) **First Token: GitHub Personal Access Token**
   1. Open a new tab and go to [GitHub Settings](https://github.com/settings/tokens)
   2. Click the blue "Generate new token" button
   3. Click "Generate new token (classic)"
   4. Fill out the form:
      ```
      Note: Course Access Token
      Expiration: No expiration
      ```
   5. Scroll down and check these boxes exactly:
      ```
      [x] repo
          [x] repo:status
          [x] repo_deployment
          [x] public_repo
          [x] repo:invite
          [x] security_events
      [x] workflow
      [x] admin:org
          [x] write:org
          [x] read:org
      ```
   6. Scroll to bottom and click "Generate token"
   7. 🚨 **IMPORTANT**: You will see a green box with your token
      - It looks like: ghp_XXXXXXXXXXXXXXXXX
      - Copy this token RIGHT NOW
      - Paste it into a safe place (Notes app, password manager)
      - You will NEVER see this token again if you leave the page!

   b) **Second Token: Organization Sync Token**
   1. In your class:
      - Ask your instructor for the "Org Sync Token"
      - They will give you a code starting with `ghp_` or `github_pat_`
      - Copy this token to the same safe place as your first token
   
   ✅ **Token Checklist**:
   - [ ] I have my GitHub Personal Access Token saved
   - [ ] I have the Organization Sync Token from my instructor
   - [ ] Both tokens are saved somewhere safe
   - [ ] I haven't shared these tokens with anyone

2. **Add Your Tokens to GitHub** (🔒 Security Setup)
   
   Now let's add these tokens to your repository:

   a) **Open Your Repository Settings**:
   1. Go to your repository on GitHub.com
   2. Click the "⚙️ Settings" tab (near the top)
   3. Look at the left sidebar
   4. Click "Secrets and variables"
   5. Click "Actions"

   b) **Add First Token** (GitHub Token):
   1. Click the green "New repository secret" button
   2. Fill in the form:
      ```
      Name: GITHUB_TOKEN
      Value: [Paste your GitHub Personal Access Token]
      ```
   3. Click "Add secret"
   4. You should see "GITHUB_TOKEN" in the list

   c) **Add Second Token** (Org Token):
   1. Click "New repository secret" again
   2. Fill in the form:
      ```
      Name: ORG_SYNC_TOKEN
      Value: [Paste the token from your instructor]
      ```
   3. Click "Add secret"
   4. You should see both "GITHUB_TOKEN" and "ORG_SYNC_TOKEN" listed

3. **Create the Sync File** (📁 File Setup)
   
   Now we'll create the file that makes everything work:

   a) **Create Folders**:
   1. Open GitHub Desktop
   2. Click "Repository" in the top menu
   3. Click "Open in Finder" (Mac) or "Open in Explorer" (Windows)
   4. In your repository folder:
      - Create a new folder called `.github`
      - Inside `.github`, create another folder called `workflows`
      
   b) **Create File**:
   1. Open any text editor (Notepad, TextEdit, VS Code)
   2. Create a new file
   3. Save it as `sync-to-org.yml` in the `.github/workflows` folder
   4. Copy and paste this exact text (every character matters!):

```yaml
name: Sync to Traders@SMU

on:
  push:
    branches:
      - main
  schedule:
    - cron: '0 0 * * *'

jobs:
  sync-to-org:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v2
        with:
          fetch-depth: 0
          
      - name: Push to Traders@SMU
        run: |
          git remote add traders-smu https://${{ secrets.GITHUB_TOKEN }}@github.com/Traders-SMU/${GITHUB_REPOSITORY#*/}.git
          git push traders-smu --all --force
          git push traders-smu --tags --force
        env:
          GITHUB_TOKEN: ${{ secrets.ORG_SYNC_TOKEN }}
```

4. **Test Your Setup** (✅ Verification)
   
   Let's make sure everything works:

   a) **Check Actions Tab**:
   1. Go to your repository on GitHub.com
   2. Click the "Actions" tab
   3. You should see "Sync to Traders@SMU" listed

   b) **Make a Test Change**:
   1. Open the README.md file in your repository
   2. Add a space at the end of any line
   3. In GitHub Desktop:
      - Type "Test sync setup" in the summary
      - Click "Commit to main"
      - Click "Push origin"
   4. Go back to the Actions tab
   5. You should see a new workflow run
   6. Wait for the green checkmark ✅

❗ **Important Token Safety Rules**:
1. **NEVER**:
   - Share your tokens with anyone (except your instructor)
   - Put tokens in your code or files
   - Post tokens in chats or emails
   - Take screenshots of tokens

2. **ALWAYS**:
   - Keep tokens in a secure place
   - Use exact names: `GITHUB_TOKEN` and `ORG_SYNC_TOKEN`
   - Tell your instructor if you think someone saw your token
   - Create new tokens if you're unsure about security

🆘 **Common Token Problems & Solutions**:

1. **"Invalid Token" Error**:
   - Check token names are exactly `GITHUB_TOKEN` and `ORG_SYNC_TOKEN`
   - Make sure you copied the entire token (they're very long)
   - Try generating a new GitHub token if needed

2. **"Permission Denied" Error**:
   - Check that all checkboxes were selected when creating the token
   - Make sure you're using the correct token in each secret
   - Ask your instructor to verify your organization access

3. **"Workflow Failed" Error**:
   - Check the Actions tab for specific error messages
   - Take a screenshot of the error
   - Send it to your instructor for help

Need help? Contact your instructor with:
1. Your repository name
2. Screenshots of any errors
3. Which step you're stuck on
4. DO NOT send your tokens!

### Step 5: Daily Usage

1. **View or Edit Files**
   - Open GitHub Desktop
   - Click on your repository
   - Click "Open in Finder/Explorer" to view files
   - Make changes to files as needed for assignments

2. **Save Your Changes (Super Easy Method)**
   - In GitHub Desktop:
     - Click the "Fetch origin" button (↓) at the top
     - Click "Pull origin" if it appears
     - Type a short note about what you changed
     - Click "Commit to main"
     - Click "Push origin" (↑)

That's it! Your work will automatically sync to the Traders@SMU organization.

### Getting Course Updates (New Super Easy Method!)

We've made it super simple to get new course materials! Just follow these steps:

1. **One-Time Setup**
   - Go to your repository on GitHub.com
   - Click the "⚙️ Settings" tab
   - Click "Actions" on the left sidebar
   - Under "General", scroll to "Workflow permissions"
   - Select "Read and write permissions"
   - Click "Save"

2. **Enable Auto-Updates**
   - Still in Settings, click "Actions" → "General"
   - Scroll to "Allow GitHub Actions to create and approve pull requests"
   - Check this box
   - Click "Save"

That's all! Your repository will now:
- Automatically check for new course materials every day
- Create a pull request when new materials are available
- Show you a notification when updates are ready
- Let you click one button to update

When you see "Updates Available" at the top of your repository:
1. Click the "Pull requests" tab
2. Click the "Update course materials" pull request
3. Click the green "Merge pull request" button

Then in GitHub Desktop:
1. Click "Fetch origin" (↓)
2. Click "Pull origin"

Done! You now have the latest course materials! 🎉

### Need Help?

If you get stuck:
1. Ask your instructor for help
2. Send screenshots of any error messages
3. Share your repository name and GitHub username

### Alternative Setup Methods

If you're comfortable with Git and GitHub, you can also:
1. Use the GitHub web interface directly
2. Use Visual Studio Code's Git features
3. Use other Git GUI clients

For advanced setup instructions, scroll down to the "Advanced Setup Options" section below.

## Receiving Updates Throughout the Course

As the course progresses, we'll add new materials for upcoming weeks (Week 2, Week 3, etc.). You'll need to update your repository to get these new materials. Here's how:

### Option 1: Using GitHub Web Interface (Easiest Method)

1. Navigate to your repository on GitHub
2. Look for the message that says "This branch is X commits behind Traders-SMU:main"
3. Click on "Sync fork" near the top of the page
4. Click "Update branch" to get the latest changes
5. Once updated online, pull the changes to your local repository:
   - In GitHub Desktop: Click "Fetch origin" then "Pull origin"
   - In Git command line: Run `git pull origin main`

### Option 2: Using Git Command Line (More Control)

First time setup (only do this once):
```bash
# Add the original repository as an "upstream" remote
git remote add upstream https://github.com/Traders-SMU/student-template.git
```

Whenever you need to get updates:
```bash
# Make sure you're on your main branch
git checkout main

# Get the latest changes from the original repository
git fetch upstream

# Merge those changes into your local repository
git merge upstream/main

# Push the updated content to your GitHub repository
git push origin main
```

### Handling Merge Conflicts

If you've modified files that were also updated in the original repository, you might see a "merge conflict." This happens when Git can't automatically determine which changes to keep.

If you encounter merge conflicts:

1. Look for files marked as conflicted in GitHub Desktop or listed in the command line output
2. Open these files in a text editor - you'll see sections marked with `<<<<<<<`, `=======`, and `>>>>>>>`
3. Edit the file to keep the changes you want (remove the marker lines and unwanted content)
4. Save the file
5. Mark the conflict as resolved:
   - In GitHub Desktop: Right-click the file and select "Mark as resolved"
   - In Git command line: Run `git add <filename>` for each resolved file
6. Complete the merge:
   - In GitHub Desktop: Click "Commit merge"
   - In Git command line: Run `git commit`

If you're unsure how to resolve conflicts, reach out to your instructor for assistance.

### When to Update Your Repository

We recommend checking for updates:
- At the beginning of each week
- Whenever an announcement is made about new materials
- If you encounter references to files that don't exist in your repository

## Common Issues and Solutions

### "Fatal: Repository not found" Error

This usually means the repository URL is incorrect or you don't have access.
- Check that you're using the correct URL
- Make sure you've created your own copy of the template repository

### "Permission denied" Error

This typically means you don't have write access to the repository.
- Make sure you're pushing to your own repository, not the original template
- Check that you've set up your GitHub authentication correctly

### Changes Not Showing Up

If your changes aren't appearing on GitHub:
- Make sure you've committed your changes (`git commit`)
- Make sure you've pushed your changes (`git push`)
- Check that you're on the correct branch

### "Updates were rejected" Error

This usually means there are changes on GitHub that you don't have locally.
- Pull the latest changes first: `git pull origin main`
- Then try pushing again

## Getting Help

If you encounter any issues:
- Ask a classmate who might be familiar with Git
- Contact your program instructor
- Search for your error message on [Stack Overflow](https://stackoverflow.com/)
- Refer to the [GitHub documentation](https://docs.github.com/en)

## Git/GitHub Terminology

- **Repository (Repo)**: A storage location for your project
- **Clone**: Creating a local copy of a repository on your computer
- **Commit**: Saving your changes to the local repository
- **Push**: Uploading your committed changes to the remote repository (GitHub)
- **Pull**: Downloading changes from the remote repository to your local copy
- **Branch**: A separate version of the repository for development
- **Pull Request (PR)**: A request to merge changes from one branch into another
- **Fork**: A copy of a repository that you manage
- **Upstream**: The original repository that you created your copy from
- **Merge**: Combining changes from different sources
- **Merge Conflict**: When Git can't automatically combine changes

Remember, everyone starts somewhere with Git! Don't be afraid to ask questions if you get stuck.

```bash
# After downloading or creating the new files
git add L1/Week2/
git commit -m "Add Week 2 materials"
git push origin main
```