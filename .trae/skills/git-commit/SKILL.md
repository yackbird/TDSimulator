---
name: "git-commit"
description: "Automates Git commit and branch workflow. Invoke when user asks to commit, switch branches, or manage Git operations."
---

# Git Workflow Automation

This skill automates Git operations for the TDSimulator project.

## Project Information

- **Remote Repository**: https://github.com/yackbird/TDSimulator.git
- **Default Branch**: main
- **Development Branch**: develop

## Trigger Conditions

Invoke this skill when:
- User says "帮我提交" (help me commit)
- User says "提交代码" (commit code)
- User says "保存修改" (save changes)
- User says "帮我切换到 X 分支" (help me switch to X branch)
- User says "切换分支" (switch branch)
- User asks to commit/push/switch branches in Git

---

## Feature 1: Commit Changes

### Step 1: Check Current Status
```bash
git status
```
Review what files have been modified and show the user what changed.

### Step 2: Ask for Commit Message
**IMPORTANT**: Always ask the user for a commit message BEFORE staging and committing.

Example prompt:
> "请告诉我您想要的 commit message？"
> 
> 例如：
> - feat: 添加新功能
> - fix: 修复bug
> - refactor: 代码重构

Wait for user's response before proceeding.

### Step 3: Stage All Changes
After user provides commit message:
```bash
git add -A
```

### Step 4: Create Commit
Use the commit message provided by user:
```bash
git commit -m '<user provided message>'
```

### Step 5: Push to Remote
Push to the corresponding remote branch:
```bash
git push
```

---

## Feature 2: Switch Branch

### Step 1: Check Current Branch
```bash
git branch
```
Show current branch and available branches.

### Step 2: Switch to Target Branch
If user specifies branch name:
```bash
git checkout <branch-name>
```

Common branches:
- `git checkout main` - switch to main branch
- `git checkout develop` - switch to develop branch

### Step 3: Pull Latest Changes (Auto)
**IMPORTANT**: Always pull latest changes after switching branches:
```bash
git pull
```

### Step 4: Confirm Success
Show current branch to confirm switch:
```bash
git branch
```

---

## Feature 3: Create New Branch

If user wants to create a new branch:
```bash
git checkout -b <new-branch-name>
```

---

## Branch Handling

- If on `develop` branch: push to `origin develop`
- If on `main` branch: push to `origin main`
- If on a feature branch: push to corresponding remote branch

## Remote Repository

If remote is not configured, add it:
```bash
git remote add origin https://github.com/yackbird/TDSimulator.git
```

---

## Example Usage

### Example 1: Commit Changes
```
User: "帮我提交"
Assistant:
1. Run `git status` to see changes
2. **Ask user**: "请告诉我您想要的 commit message？"
3. User responds: "feat: 添加新功能"
4. Run `git add -A` to stage
5. Run `git commit -m 'feat: 添加新功能'`
6. Run `git push` to push to remote
```

### Example 2: Switch Branch
```
User: "帮我切换到 develop 分支"
Assistant:
1. Run `git branch` to show current branch
2. Run `git checkout develop`
3. Run `git pull` to update latest code
4. Run `git branch` to confirm
5. Tell user: "已切换到 develop 分支，代码已更新"
```

### Example 3: Switch to Main
```
User: "帮我切换到 main 分支"
Assistant:
1. Run `git checkout main`
2. Run `git pull` to update latest code
3. Tell user: "已切换到 main 分支，代码已更新"
```

---

## Notes

- Always check current branch with `git branch`
- If network fails, remind user to push manually later
- Keep commit messages concise and descriptive
- Remote URL: https://github.com/yackbird/TDSimulator.git
- Before switching branches, remind user to commit or stash changes if there are uncommitted changes
