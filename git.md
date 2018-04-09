# Collection of Git commands

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

Add files interactively:

```
git add -p
```
## Stashing

Save un-commited work. The stash is safe from destructive operations. 

```
# stash changes
git stash
git stash save "WIP: making progress on foo"

# list changes
git stash list

# remove the last stash and apply changes (does not remove if there's merge conflict)
git stash pop

# keep untracked files
git stash --include-untracked
```

## Tag

```
git tag -a v1.0 -m "Version 1.0"

# list all tags
git tag
git show-ref --tags
# show a tag
git show <tagname>
```

## Edit configuration

```
git config --global -e
```

## [Associating text editors with Git](https://help.github.com/articles/associating-text-editors-with-git/):

Sublime:
```
git config --global core.editor "subl -n -w"
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