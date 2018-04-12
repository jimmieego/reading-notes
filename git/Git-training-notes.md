# Git training notes

04/11/2018

## Repo

- http://github.com/githubschool/data-hearing

## Scripts

- http://github.com/github/training-utils
- http://github.com/github/training-kit

## Resources

- http://github.com/works-with
- http://git-school.github.io/visualizing-git

## Notes

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
- Github always does `git merge --no-ff <branch>`. Note there is a merge commit in order to show the pull request.
- Every time you start working, do a `git pull` first.
- Rules for merge conflict:
  - On the feature branch with conflicts, do `git merge master`.
  - Resolve the conflicts.
  - Push resolved changes.
  - Merge on Github UI.
- `git bisect`: https://git-scm.com/docs/git-bisect
- `git add -p`: select changes to be added to staging
- See differences:
  - `git diff`: difference between working and staging
  - `git diff --staged`:
  - `git diff HEAD`
- `git commit --amend`: use it in local branch.
- `git reflog` to view local commit history
- `git cherry-pick <commit-sha1>`

## Rebase

Rebasing at its simplest is moving the head of your local branch to the head of the branch you are rebasing onto, then applying any commits you have added locally onto the new head.

The number one rule when rebasing is to NOT rebase commits that have been pushed to a remote branch already, only rebase in your **local** branch before pushing to remote.

Rebase is very useful when you need ensure you have the latest code in the local branch you are working on.

A good example of this is when the fix you are working on needs a fix someone else applied after you created your branch. It is also extremely useful to rebase before pushing your commits to remote for a pull request, as you will ensure locally that your commits will be able to merge without conflict before creating the pull request.

For example, if you have a local branch `bugfix` and you want to rebase it onto the latest from `master`:

- Checkout the local branch you want to rebase: `git checkout bugfix`
- Fetch the latest from master: `git fetch origin master`
- Rebase the local branch onto the latest from master: `git rebase origin/master`
- Fix any merge conflicts locally
- Push your branch to remote so you can create a pull request: `git push -u origin bugfix`

`git rebase -i origin/master`: Rebasing interactively allows you to squash commits together, rewrite commit messages, drop commits, and more. This is especially useful if you have many commits that can apply to a single bug fix or feature over the course of time you worked on it, and want to consolidate those commits into a single commit with a clear commit message.

`git rebase --abort`: throw away the attempt at reabasing.

## Helpful commands

### Ignore changes to a file

```git
git update-index --assume-unchanged <path/to/file>

# reverse
git update-index --no-assume-unchanged <path/to/file>
```

### Restoring a local branch that you've deleted

If you've deleted a local branch by accident or for some other reason need to recover it, you just need to know the SHA1 id that was at the tip of your branch when you deleted it. This SHA1 id is displayed when you delete your branch, when git displays "Deleted branch [branchname] (was [sha1])". You can also use `git reflog` to find the commit that was at the tip of the branch you deleted. 

Once you have that SHA1 id, simply run the command, `git checkout -b [branchname] [sha1]`.