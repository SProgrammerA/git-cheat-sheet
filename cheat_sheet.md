# 📝 Git Cheat Sheet – Daily Workflow & SSH Signing

A **personalized Git cheat sheet** focusing on **daily workflow commands, branch management, SSH commit/tag signing**, and other essential Git operations.  

This cheat sheet is practical, concise, and ready for reference while coding.  

---

## 📑 Table of Contents

1. [Daily Essentials](#1--daily-essentials)  
2. [Working with Remotes](#2--working-with-remotes)  
3. [Fixing Mistakes](#3-fixing-mistakes)  
4. [Feature Branch Workflows](#4--feature-branch-workflows)  
5. [Stashing Work](#5--stashing-work)  
6. [Git Show – Inspect Commits, Changes & Tags](#6--git-show--inspect-commits-changes--tags)  
7. [Searching](#7--searching)  
8. [Aliases / Quality-of-Life Commands](#8--aliases--quality-of-life-commands)  
9. [Optional Advanced Commands](#9-optional-advanced-commands)  
10. [SSH Keys & Signing](#10--ssh-keys--signing)  
11. [Signing Commits & Tags with SSH](#11--signing-commits--tags-with-ssh)  
12. [Allowed Signers File](#12-ssh-allowed-signers-file)  

---

## 1. 📌 Daily Essentials

### **Check What’s Going On**
```
git status
git log --oneline --graph --decorate
git diff
```

### **Stage & Commit**

```
git add .             # add all changes
git add <file>        # add specific file
git commit -m "msg"
git commit --amend    # edit last commit
```

### **Branches**

```
git branch             # list local branches
git branch -a          # list all branches
git checkout <branch>  # switch branch
git switch <branch>    # modern alternative
git switch -c <name>   # create + switch
```

### **Updating Your Branch**

```
git pull               # fetch + merge
git pull --rebase      # cleaner history
git fetch              # fetch only
```

---

## 2. 🚀 Working with Remotes

```
git push
git push -u origin <branch>  # set upstream

git remote -v
git remote add origin <url>
git remote set-url origin <url>
```

---

## 3. Fixing Mistakes

### **Undo Staging**

```
git restore --staged <file>
```

### **Undo Working Directory Changes**

```
git restore <file>
```

### **Reset to a Commit**

```
git reset --soft <commit>   # keep changes staged
git reset --mixed <commit>  # keep changes unstaged (default)
git reset --hard <commit>   # lose changes
```

### **Revert a Commit (Safe, Keeps History)**

```
git revert <commit>
```

---

## 4. 🌱 Feature Branch Workflows

### **Rebase (Clean History)**

```
git rebase main
git rebase -i HEAD~5      # interactive rebase
```

### **Merge**

```
git merge <branch>
```

---

## 5. 📦 Stashing Work

```
git stash
git stash pop
git stash list
git stash apply stash@{1}
```

---

## 6. 🔍 Git Show – Inspect Commits, Changes & Tags

### **Show a commit**

```
git show <commit>
```

### **Show summary only**

```
git show --stat <commit>
```

### **Show a specific file in a commit**

```
git show <commit>:<path/to/file>
```

### **Show a tag**

```
git show <tagname>
```

### **Additional useful options**

```
git show --pretty=fuller <commit>
git show --name-only <commit>
git show --patch-with-stat <commit>
```

---

## 7. 🔎 Searching

```
git grep "<text>"           # search in tracked files
git log -S "<text>"         # search commits that added/removed text
```

---

## 8. ✨ Aliases / Quality-of-Life Commands

```
git config --global alias.st "status -sb"
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.lg "log --oneline --graph --decorate --all"
```

---

## 9. Optional Advanced Commands

```
git blame <file>
git show --name-only <commit>
git clean -fd
```

---

## 10. 🔐 SSH Keys & Signing

### **Generate SSH key**

```
ssh-keygen -t ed25519 -C "your_email@example.com"
# or RSA if needed
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

### **Start ssh-agent & add key**

```
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

### **Copy public key**

```
cat ~/.ssh/id_ed25519.pub
```

---

## 11. 🔏 Signing Commits & Tags with SSH

### **Enable SSH commit signing globally**

```
git config --global gpg.format ssh
git config --global user.signingkey ~/.ssh/id_ed25519.pub
git config --global commit.gpgsign true
git config --global tag.gpgsign true
```

### **Sign a commit**

```
git commit -S -m "message"
```

### **Verify a signed commit**

```
git verify-commit <commit>
```

### **Create a signed tag**

```
git tag -s v1.0.0 -m "Release v1.0.0"
```

### **Verify a signed tag**

```
git verify-tag v1.0.0
```

### **Push signed tag**

```
git push origin v1.0.0
```

---

## 12. SSH Allowed Signers File

### **Create allowed signers file**

```
mkdir -p ~/.ssh
touch ~/.ssh/allowed_signers
```

### **Add your public key**

```
echo "your_email@example.com $(cat ~/.ssh/id_ed25519.pub)" >> ~/.ssh/allowed_signers
```

### **Tell Git where the file is**

```
git config --global gpg.ssh.allowedSignersFile ~/.ssh/allowed_signers
```

### **Test verification**

```
git verify-commit <commit>
git verify-tag <tagname>
```

---

# 🎉 **Happy Coding!**
