
## 1. Setup & Initialization

|Command|Description|
|---|---|
|`git init`|Initializes a new local Git repository in the current folder.|
|`git clone [url]`|Downloads a project and its entire version history from GitHub.|
|`git config --global user.name "[name]"`|Sets the name you want attached to your commit transactions.|
|`git config --global user.email "[email]"`|Sets the email you want attached to your commit transactions.|

---

## 2. The Staging Area & Committing

|Command|Description|
|---|---|
|`git status`|Lists all new or modified files to be committed.|
|`git add [file]`|Snapshots the file in preparation for versioning (Staging).|
|`git add .`|Stages **all** changed files in the current directory.|
|`git commit -m "[message]"`|Records file snapshots permanently in version history with a descriptive message.|

---

## 3. Branching & Merging

|Command|Description|
|---|---|
|`git branch`|Lists all local branches in the current repository.|
|`git branch [branch-name]`|Creates a new branch.|
|`git checkout [branch-name]`|Switches to the specified branch and updates the working directory.|
|`git checkout -b [branch-name]`|Shortcut to create a new branch and switch to it immediately.|
|`git merge [branch]`|Combines the specified branch's history into the current branch.|

---

## 4. Synchronizing with GitHub (Remote)

| Command                       | Description                                                     |
| ----------------------------- | --------------------------------------------------------------- |
| `git remote add origin [url]` | Links your local repository to a remote GitHub repo.            |
| `git fetch`                   | Downloads all history from the remote tracking branches.        |
| `git pull`                    | Fetches and merges any commits from the tracking remote branch. |
| `git push origin [branch]`    | Uploads all local branch commits to GitHub.                     |


---

## 5. Inspecting & Undoing

|Command|Description|
|---|---|
|`git log`|Shows the commit history for the currently active branch.|
|`git diff`|Shows file differences not yet staged.|
|`git reset [file]`|Unstages the file, but preserves its contents.|
|`git revert [commit-id]`|Creates a new commit that undoes the changes of a previous commit without deleting history.|
