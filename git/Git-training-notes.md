Repo:

- http://github.com/githubschool/data-hearing

Scripts:

- http://github.com/github/training-utils
- http://github.com/github/training-kit

Resources:

- github.com/works-with

Notes:

- Create branch remotely first and pull down. The remote branch will be auto tracked.
- Commit message: be descriptive.
- Create PR: Use Pull Requests tab > New Pull Request button.
- `git remote prune origin` deletes all stale remote-tracking branches.
- `git pull --prune` to remove stale branches for remote branches that have been deleted. Set `git config --global fetch.prune true` to be the default behavior of `git pull`.
- `git branch -d -r origin/coolbranch` deletes a particular remote-tracking branch.
- `git log` page view commands:

    ```git
    Next line:  return
    Next page:  space bar
    Previous page:  w
    Quit viewing the diff:  q
    Help:  h
    ```
  - `git log --oneline`
  - `git log --oneline --graph`
  - `git log --oneline --graph --decorate --all`
- Set up aliase: `git config --global alias.lol "log --oneline --graph --decorate --all"`
  - Unset: `git config --global --unset alias.lol`
  - [GitHub Flow Like a Pro with these 13 Git Aliases](https://haacked.com/archive/2014/07/28/github-flow-aliases/)
  - `git config --global --list` to see all aliases.