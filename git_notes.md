# Git Notes

Author: __*yufanana*__
</br>
____

## General

`git <verb>` 

`git <verb> --help` get documentation about \<verb>.

From 2023, you will need to add SSH keys generated on your computer to your GitHub account in order to access the repositories.

## Best Practices

- Main branches should be stable and ready for production. Changes are only merge after review and testing.
- Use hyphens and slashes as separators
    - `feature/new-user-login`
- Possible branch naming conventions, choose one.
    - start with group words like `feature/`, `bugfix/`, `wip/`, `exp/`
    - include author names `john/add-bot`

## Staging

<img src="./notes_images/git_map.jpg" width="500">

<br>

| Basic Commands     | Description                                            |
| ------------------ | ------------------------------------------------------ |
| `git status`       | Lists which files are staged, unstaged, modified.      |
| `git add file.py`  | Adds the file to the staging area.                     |
| `git add .`        |  adds all the files in the folder to the staging area. |
| `git stage`        | Synonymous with `git add .`                            |
| `git commit -m "commit msg"`| Commit changes to the current branch.|
| `git push` <br> `git push origin main` <br> `git push other_repo feature1`    | Pushes commits to the branch in remote repository.      |
| `git pull` <br> `git pull origin main` <br> `git pull other_repo main` | Pull/download changes from the remote origin. |

Note: `origin` is the name of the remote repository. See section on Git Remote.

## Manipulating Commits

This section should be skipped if you are new to Git.

| Advanced Commands     | Description                                         |
| ------------------ | ------------------------------------------------------ |
|`git diff`           | Shows the changes made.                               |
| `git reset`         | Removes everything from the staging area.             |
| `git reset file.py` | Removes file only from the staging area.              |
|`git reset --soft HEAD~1` | Removes everything from the commit into the staging area. |
|`git log` <br> `git log --oneline` <br> `git log --oneline --graph` | Show the history of commits as oneline or a tree graph |
|`git log --after="2021-7-1"` <br> `git log --before="2021-6-1"` <br> `git log --author="John"` <br> `git log --grep="fix"` <br> `git log -- file.py`| Search for commits based on search criteria (can be combined). |
|`git commit --amend` <br> `git commit --amend -m "updated msg"` <br> `git commit --amend --no-edit`| Modify the most recent commit.|
|`git reflog`         | Open the reference log of important actions         |
|`git branch recover e5b19e4`  | Create new branch starting with the state hash.|
|`git cherry-pick 26bf1b48`   | To move a single commit to the current branch.  |

## Git Clone

Go to the GitHub website, select Clone, and copy the https or SSH URL.

- https URL: pushing to origin not allowed
- SSH URL:requires SSH keys added to your GitHub account, write permissions if the user has been added as a ccontributor.

`git clone <url>` makes a copy in the current directory.

## Git Remote

Go to GitHub web and create a new repositary there. Follow the instructions there to add origin.

| Commands           | Description                                            |
| ------------------ | ------------------------------------------------------ |
| `git remote -v`      | View the remote origins added.   | 
|`git remote add <origin_name> <url>` | Add a new remote. |
|`git remote rename old_name new_name`| Rename an origin. |
|`git remote set-url origin <url>`    | Change the Git origin remote.  |

## Git Ignore

- Create a `.gitignore` file in the root folder of the repository.
- Write the names of the files for *git* to ignore inside the *gitignore* file.
- Folders can be added as `/<folder directory>`
- `*.txt` to include all *.txt* files inside `.gitignore`.

Sample `.gitiginore` file below.
```
# Workspace
.vscode

# Python
__pycache__
.venv/

# Media
*.pdf
*.jpg
*.png

# Autogenerated folders
output/
build/
install/
log/
```

## Procedure from new local Repo to Remote Repo

First, create a new repo on GitHub without any README, license or gitignore files.

Sample workflow.

```bash
git init -b main
git add .
git commit -m "Initial commit"
git remote set-url origin https://github.com/username/repository.git
git push -u origin main
```

## Git Branch

| Commands           | Description                                            |
| ------------------ | ------------------------------------------------------ |
|`git branch`       | Lists all the local branches, with * as the active branch.|
|`git branch -a`    | Lists all the branches, remote and local.               |
|`git checkout feature1` | Change to the feature1 branch.                     |
|`git branch feature2` | Creates a new branch called feature2.                |
|`git branch -M old_name new_name`| Rename a branch.                          |
|`git branch --merged` | List branches that have been merged so far.          |

Any commits to the local branch has no effect on local main branch or remote repo, and should be pushed by doing `git push`.

## Git Merge

`git merge <branch_name>` merges the specified branch to the active branch, which is `main` in this case.

Sample Workflow

```bash
git checkout main
git pull origin main
git merge feature1
git push origin main
```

Once merge is successful,  

`git branch -d <branch_name>` to delete branch locally.  

`git push origin --delete <branch_name>` to delete branch in remote repo.  

## Git Rebase

Do not use interactive rebase on commits that have been pushed to a shared repository. Used for cleaning local history commit before pushing.

`git rebase -i HEAD~3` to have an interactive window including up to 3 commits before. Think of `~` as minus.

- `squash`: combines 2 commits into 1
- `reword`: change commit message
- `edit`, `pick`, `drop`, `reset`, etc.

## Git Submodules

To include a Git repo inside another git repo. The submodule should not be modified. It clones the current version/commit of the git repo.  

| Commands           | Description                                            |
| ------------------ | ------------------------------------------------------ |
|`git submodule add <url>`| Add the repo as a submodule to the local repo.    |
|`git submodule update --init --recursive` | To set up the submodules in your repository.|
