# First change - Clone, Branch, Commit, Push & Pull request

This is the basic commands you need to be able to use Git to make a basic change to any repository. There is also examples for using VS Code for some of this to make it easier to use.

## Clone repository

- [GitHub clone repository](https://learn.microsoft.com/en-us/azure/devops/repos/git/clone?view=azure-devops&tabs=visual-studio-2022)
- [Azure DevOps clone repository](https://learn.microsoft.com/en-us/azure/devops/repos/git/clone?view=azure-devops&tabs=visual-studio-2022)

Using Git Bash:

```bash
git clone <repo>
```

Using VS Code:

- This isn't really possible using VS Code so I recommend you use Git Bash.

## Git overview

Definition from Wikipedia:

> Git is a distributed version control system that tracks versions of files. It is often used to control source code by programmers who are developing software collaboratively.

Git uses references (ref) to point to a set of files and file changes. Each commit create a new ref using a SHA-1. This can be shortened to a 7 length hex value e.g. `8ec9f51`.

A branch in is a pointer to a specific ref. When you commit to a branch, it moves the pointer to the new commit. Each time you add a commit, the pointer moves creating a tree of commits. By running the `git tree` alias you can see this. Below I created a branch called `example` then committed to that branch twice. Newest commits are always the newest commit. `HEAD` is a special tag that always points to your current commit ref.

```bash
* 8ec9f51 (HEAD -> example) Commit 2
* 231c7fd Commit 1
* c0bc923 (origin/main, origin/HEAD, main) Initial Commit
```

The value in brackets is the branch name - `main`. Branches that start with `origin/` are the upstream tracking branch. This is where the branch is located in the upstream repository. You can update this by running `git fetch` to get the latest upstream information.

## Switch branches

There is a few ways to do this, but I recommend using the `switch` command. Make sure you are on the branch you want to base your branch on. This is normally the `main` branch. The new branch will always be created off whatever `HEAD` points to locally. If you switch to a branch `HEAD` will always point to the latest commit on the branch. Either method works well, but usually us VS Code.

Using Git Bash:

```bash
git switch -c <branch>
```

Using VS Code:

- [VS Code - Branches](https://code.visualstudio.com/docs/sourcecontrol/overview#_branches-and-tags)
  - On the Git panel.
  - If you have a single folder you need to look at the bottom left, click on `main`.
  - Then click `+ Create new branch...`.
  - Then type a name.

## Stage & unstage file(s)

Recommend you use VS Code for this, as it has a more user friendly approach.

On the right side of changes in the Git panel in VS code

- To stage file(s) by pressing the `+` button.
- To un-stage file(s) by pressing the `-` button.

To use Git Bash, you can use these commands:

Add all locally changed files that are not ignored by [.gitignore](https://docs.github.com/en/get-started/getting-started-with-git/ignoring-files):

```bash
# Add all locally changed files that are not ignored by .gitignore
git add .

# To add specific file
git add <file>
```

To un-stage files use these commands:

```bash
# To un-stage all files
git reset .

# To un-stage a specific file
git add <file>
```

## Commit file

To commit, you can use Git Bash or VS Code. Some functionality is easier using Git Bash, so its best to get comfortable using Git Bash.

Using Git Bash:

```bash
git commit -m "Commit Message"
```

Using VS Code:

- On the Git panel.
- Type the "Commit Message" in the message field.
- Then press the `tick icon` to commit

## Push changes upstream

Push behaves differently depending on some settings you set when you installed Git. If you have set the autoSetupRemote, then you should be able to just run git push

```bash
# Set this once
git config --global push.autoSetupRemote true

# Then just run
git push
```

If you don't use set autoSetupRemote, then you need to set the upstream the first time you push. Like below, then `git push` will work from that point on.

```bash
# If you don't have autoSetupRemote
git push --set-upstream origin <branch>
```

## Create pull request

You then need to create a pull request, the instructions depends on where your Git repository is stored.

- [GitHub pull request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request)
- [Azure DevOps pull request](https://learn.microsoft.com/en-us/azure/devops/repos/git/pull-requests?view=azure-devops&tabs=browser)
- [GitLab merge request](https://docs.gitlab.com/ee/user/project/merge_requests/creating_merge_requests.html)
