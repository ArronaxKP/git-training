# Cheat sheet

Here are some common useful cheat sheets to use as reference:
- [GitHub](https://education.github.com/git-cheat-sheet-education.pdf)
- [Atlassian](https://www.atlassian.com/git/tutorials/atlassian-git-cheatsheet)
- [GitLab](https://about.gitlab.com/images/press/git-cheat-sheet.pdf)

## My cheat sheet

This is my specific cheat sheet:

### Setup

- `git config --global user.name "John Doe"` - Set Git user name.
- `git config --global user.email johndoe@example.com` - Set Git email address.
- `git config --global alias.tree "log --graph --decorate --pretty=oneline --abbrev-commit"` - Set alias for `git tree`.

### Common commands

- `git clone https://<repo>` - Clone repository at URL `https://<repo>`.
- `git switch main` - switch to the main branch.
- `git switch -c <branch>` - Switch to your own branch, and create it.
- `git add .` - Stage all locally changed files (not excluded by `.gitignore`).
- `git reset <filename>` - Un-stage all files.
- `git add <filename>` - Stage a specific file.
- `git reset <filename>` - Un-stage a specific file.
- `git commit -m "Commit Message"` - Commit the changes.
- `git push` - Push changes to upstream repository.
- `git pull --rebase` - Update your branch with upstream changes.

### Advanced commands

- `git rebase -i HEAD~3` - Rebase the last 3 commits.
