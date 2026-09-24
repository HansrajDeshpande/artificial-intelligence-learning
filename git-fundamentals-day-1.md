# Git Fundamentals — Day 1

This document covers the Git concepts and commands learned today. It intentionally focuses on Git itself; GitHub-specific concepts are included only where necessary to explain Git's remote-repository workflow.

---

## 1. What is Git?

Git is a distributed version control system used to track changes to files over time. It records a history of changes so you can understand how a project evolved and can return to earlier versions when necessary. Git works primarily on your local computer, so creating commits and reviewing history does not require an internet connection. Git can be used for personal projects as well as collaborative software development.

---

## 2. Git Repository

A Git repository is a project whose files and version history are managed by Git. When Git is initialised in a directory, it creates a hidden `.git` directory containing the information Git needs to track the project. The repository includes the project's working files and Git's internal version-control data. A repository can exist entirely on your computer or can be connected to one or more remote repositories.

---

## 3. Working Directory

The working directory is the set of project files you are currently working on. When you create, edit, rename, or delete files, those changes initially occur in the working directory. Git compares the working directory with the tracked state of the repository to identify changes. This is the area where your normal development and editing takes place.

---

## 4. `.git` Directory

The `.git` directory is the internal directory created by Git for a repository. It contains information such as commit objects, references, branch information, and repository configuration. It is what allows Git to maintain the project's history and understand its different states. You normally should not manually edit or delete anything inside `.git`.

To view it:

```bash
ls -la
```

---

## 5. Staging Area

The staging area is an intermediate area where you select changes that should become part of the next commit. It allows you to choose exactly which changes will be included rather than automatically committing every modification in your working directory. The `git add` command moves changes into the staging area. The staging area is therefore the bridge between your working directory and the commit you are preparing.

```text
Working Directory
       |
       | git add
       v
Staging Area
       |
       | git commit
       v
Repository History
```

---

## 6. Commit

A commit is a recorded snapshot of the changes that were staged at that point in time. Every commit has a unique identifier and normally includes a message describing the change. Commits form the history of a Git repository and allow you to inspect how the project changed over time. A commit is created locally and is not automatically transferred to a remote repository.

Example:

```bash
git commit -m "Add Git introduction"
```

---

## 7. Branch

A branch is a movable reference to a line of development in a Git repository. Branches allow different changes to be developed independently without requiring all work to happen on the same line of history. A repository can contain multiple branches, with one branch checked out as the current branch. We will study branch creation, switching, merging, and conflict resolution in more detail tomorrow.

To list branches:

```bash
git branch
```

---

# Git Commands Learned Today

## 8. `git status`

`git status` shows the current state of your working directory and staging area. It identifies files that are untracked, modified, staged, or otherwise different from the current commit. It also shows the branch you are currently working on and may indicate whether the branch differs from its remote counterpart. It is one of the most useful Git commands because it tells you what Git currently sees before you perform another operation.

```bash
git status
```

---

## 9. `git add`

`git add` places changes from the working directory into the staging area. It does not create a commit and does not permanently save the changes in Git history. You can stage a specific file or multiple files depending on what you want the next commit to contain. Staging gives you control over which changes are included in the next commit.

Examples:

```bash
git add git-learning.md
```

or:

```bash
git add .
```

---

## 10. `git commit`

`git commit` records the changes currently in the staging area as a new commit in the repository's history. The commit contains the staged snapshot and a message describing the purpose of the change. A good commit should represent a meaningful unit of work and have a clear message. Creating a commit does not automatically send it to a remote repository.

Example:

```bash
git commit -m "Add Git fundamentals"
```

---

## 11. `git log`

`git log` displays the history of commits in the repository. It can show information such as commit identifiers, authors, dates, and commit messages. The `--oneline` option provides a shorter format that is useful for quickly reviewing the history. Git history is particularly useful when investigating when and how a change was introduced.

Examples:

```bash
git log
```

```bash
git log --oneline
```

---

## 12. `git diff`

`git diff` shows differences between versions of files. With no additional arguments, it normally shows changes in the working directory that have not yet been staged. It is useful for reviewing your changes before running `git add`. Reviewing the diff helps identify accidental edits, missing changes, or unwanted modifications before they become part of a commit.

Example:

```bash
git diff
```

---

## 13. `git push`

`git push` transfers commits from your local repository to a configured remote repository. It is commonly used after creating one or more local commits when you want those commits to be available in the remote copy of the repository. The command does not create a commit itself; the commit must already exist locally. In a collaborative workflow, pushing allows other people working with the remote repository to obtain your committed changes.

Example:

```bash
git push
```

---

## 14. `git pull`

`git pull` obtains changes from a remote repository and integrates them into the current local branch. It is commonly used when the remote repository contains commits that are not yet present locally. Conceptually, `git pull` combines a fetch operation with an integration operation, usually a merge or rebase depending on the configuration and options being used. Understanding `git fetch` separately will make the behaviour of `git pull` clearer, which we will cover later.

Example:

```bash
git pull
```

---

## 15. `git remote -v`

A remote is a named reference to another copy of a Git repository. `git remote -v` displays the configured remote names and their associated URLs. A remote is often named `origin` when a repository is cloned from another repository. Remotes allow Git to exchange commits between your local repository and another repository.

Example:

```bash
git remote -v
```

Typical output may look like:

```text
origin  <repository-url> (fetch)
origin  <repository-url> (push)
```

---

## 16. `git branch`

`git branch` lists the local branches in the repository and identifies the branch that is currently checked out. Branches allow you to maintain separate lines of development. The command can also be used for branch management, although `git switch` is often clearer for changing branches. We will practise branch operations in the next Git learning session.

Example:

```bash
git branch
```

---

## 17. `git clone`

`git clone` creates a new local copy of an existing Git repository. It downloads the repository's files and Git history and normally configures a remote named `origin` pointing to the source repository. After cloning, the new directory is a normal Git repository that you can work with using commands such as `git status`, `git add`, `git commit`, and `git push`. Cloning is normally the starting point when you want to obtain an existing repository for local development.

Example:

```bash
git clone <repository-url>
```

---

# The Git Workflow Learned Today

The fundamental Git workflow is:

```text
1. Create or modify files
             |
             v
2. git status
             |
             v
3. git diff
             |
             v
4. git add
             |
             v
5. Staging Area
             |
             v
6. git commit
             |
             v
7. Local Git History
             |
             v
8. git push
             |
             v
9. Remote Repository
```

When changes from the remote repository need to be brought into your local branch, `git pull` can be used.

```text
Remote Repository
       |
       | git pull
       v
Local Repository
```

---

# The Most Important Mental Model

The most important concept learned today is the difference between the working directory, staging area, and committed repository history.

```text
                 YOUR COMPUTER

       Working Directory
       (files you edit)
               |
               | git add
               v
          Staging Area
       (changes selected
        for next commit)
               |
               | git commit
               v
       Git Repository
        (commit history)
               |
               | git push
               v
        Remote Repository
```

The key sequence to remember is:

```bash
git status
git diff
git add .
git commit -m "Describe the change"
git push
```

And when you need to obtain remote changes:

```bash
git pull
```

---

# Day 1 Git Checklist

- [ ] Understand what Git is
- [ ] Understand what a Git repository is
- [ ] Understand the working directory
- [ ] Understand the `.git` directory
- [ ] Understand the staging area
- [ ] Understand commits
- [ ] Understand branches at a basic level
- [ ] Understand remotes
- [ ] Use `git status`
- [ ] Use `git add`
- [ ] Use `git commit`
- [ ] Use `git log`
- [ ] Use `git diff`
- [ ] Use `git push`
- [ ] Use `git pull`
- [ ] Use `git remote -v`
- [ ] Use `git branch`
- [ ] Understand `git clone`
- [ ] Complete the basic Git workflow without relying on a command list

---

# Commands Covered Today

```bash
git status
git add
git commit
git log
git log --oneline
git diff
git push
git pull
git remote -v
git branch
git clone
```

Tomorrow's Git topics can build on this foundation with branches, `git switch`, merging, merge conflicts, `git fetch`, `.gitignore`, reverting changes, resetting changes, and other practical Git operations.
