### Resetting remote to a certain commit

```bash
git reset --hard <commit-hash>
git push -f origin master
```

현재설정된 원격저장소 URL보기

```bash
git remote get-url origin
```

### Change the Author of commit

```bash
# copy the commit hash to be amended
git log

# create new commit with the amended author
git commit --amend --author="[name] <[email]>" -C [commit_hash]

# Force push
git push -f
```

## Basic Git Commands

```
git clone
git init
git add
git commit
git push
git pull
```

## Git aliases

```
git config --global alias.co checkout
git config --global alias.ci commit
git config --global alias.br branch
git config --global alias.st status
```

## Git Meld

```
sudo apt install meld
git config --global diff.tool git-meld
git difftool commit1 commit2 -- path/to/file
```

## Git Stash

```
git stash   // Hide the changes
git stash pop // Active the stash changes
git stash drop // Remove the stash changes
```

## Export the modified files into Zip file

```
git archive --output=changes.zip HEAD $( git diff --name-only HEAD~ HEAD --diff-filter=ACMRTUXB)
```

## Git Revert

```
git log
git reset SC06SD
```

## Git Branch

```
git branch develop  // create `develop` branch
git checkout develop    // switch to `develop` branch
```

git remote add #repo name #url

For ex: git remote add origin https://github.com/huangxiaoxuan/test.git

git reset --hard // reset about the modified file

git clean -f // reset about the created file

git checkout #hash

git push --set-…..
git rm --cached `git ls-files -i -c --exclude-from=.gitignore`
