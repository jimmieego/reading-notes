# Collection of Git knowledge

## Commit

- Commit message is in future tense.
- Short subject, followed by a blank line.
- A description of the current behavior, a short summary of **why** the fix is needed. Mention side effects.

Look at a commit:

- `git show <commit>`: show commit and contents
- `git show <commit> --stat`: show files changed in commit
- `git show <commit>: <file>`: look at a file from another commit

View unstaged changes:

```
git diff
```

View staged changes:

```
git diff --staged
```

Show changes only in branch `B`:

```
git diff A B
```

## Branch

Create a branch that points to the last commit you made in a detached state

```
git branch <new-branch-name> <commit>
```

## Merge

To retain the history of a merge commit, even if there are no changes to the base branch (no fast forward):

```
git checkout master
git merge <feature-branch-name> --no-ff
```

Which branches are merged with `master`, and can be cleaned up?

```
git branch --merged master
```

Which branches aren't merged with `master` yet?

```
git branch --no-merged master
```

## Log

```
git log --since="yesterday"
git log --since="2 weeks ago"

# log files that have been moved or renamed
git log --name-status --follow -- <file>

# search for commit messages that match a regular expression
# can be mixed & matched with other git flags
git log -grep <regexp>

```

`^n`, n: the nth parent commit
`~n`, n: number of commits back

## Files

- Add a file to the next commit:

```
git add <filename>
```

- Delete a file in the next commit:

```
git rm <file>
````

- Rename a file in the next commit:

```
git mv <file>
```

- Add files interactively:

```
git add -p
```

## Stashing

Save un-commited work. The stash is safe from destructive operations.

- stash changes

```
git stash
git stash save "WIP: making progress on foo"
```

- List changes:

```
git stash list
```

- Remove the last stash and apply changes (does not remove if there's merge conflict):

```
git stash pop
```

- Keep untracked files:

```
git stash --include-untracked
```

## Tag

- Create tag

```
git tag -a v1.0 -m "Version 1.0"
```

- List all tags:

```
git tag
git show-ref --tags
```

- Show a tag:

```
git show <tagname>
```

## Checkout

Overwrite the working area file with the staging area version from the last commit. This operation overwrites files in the working directory without warning.

```
git checkout -- <file_path>
```

Checkout a file from a specific commit. Copies to both working area and staging area.

```
git checkout <commit> -- <file_path>
```

Restore a deleted file

```
git checkout <deleting_commit>^1 -- <file_path>
```

## Clean

Clear working area by deleting untracked files:

```
git clean
```

Use `--dry-run` to see what would be deleted. Use `-f` to do the deletion. Use `-d` to clean both files and directories.

## Reset

Reset is another command that performs different actions depending on arguments: with path, without a path. By default, git reset performs `git reset --mixed`.

- For commits: moves the `HEAD` pointer, optionally modifies files
- For file paths: does not move the `HEAD` pointer, modifies files

For commits:

- `git reset --soft HEAD~`: Move HEAD and current branch
- `git reset HEAD~` or `git reset --mixed HEAD~`: Move HEAD, copy files to stage
- `git reset --hard HEAD~`: Move HEAD, copy files to stage & working; this operation cannot be undone. Do NOT push this to shared repo (change history).

In case of an accidental `git reset`, Git keeps the previous value of HEAD in variable called `ORIG_HEAD`. To go back to the way things were:

```
git reset ORIG_HEAD
```

For file:

`git reset <commit> -- <file>`: reset the staging area.

### Revert

The "safe" reset. Creates a new commit that introduces the opposite changes from the specified commit. The original commit stays in the repository. 

Use revert if you're undoing a commit that has already been shared.

Revert does not change history.

```
git revert <commit>
```

## Edit configuration

```
git config --global -e
```

## Clone submodules

If the repo contains submodules, and you want to bring the code in the submodules down, you'll need to clone recursively.

```
git clone --recursive <submodule URL>
```

## Show remote URL

Show remote URL for "origin":

```
git remote get-url origin
```

If the remote has moved, you can change the URL using `set-url`:

```
git remote set-url origin <new remote URL>
```

## Delete branch

Delete the remote branch:

```
git push -d <remote_name> <branch_name>
git push -d origin my-feature-branch
```

Delete the local branch:

```
git branch -d <branch_name>
```

## Delete local changes

Undo all unstaged local changes:

```
git checkout .
```

Undo `git add` for at single file:

```
git reset folder/filename
```

Undo `git add .`:

```
git reset .
```

## Fix untracked files

```
git rm . -r --cached
git add .
git commit -m "Fixed untracked files"
```