# Quick excercise - Remote repos and Upstream branch

## Used commands

- [_git remote -v_](https://git-scm.com/docs/git-remote#Documentation/git-remote.txt--v)
- [_git remote add `<shortname> <url>`_](https://git-scm.com/docs/git-remote#Documentation/git-remote.txt-emaddem) 
- [_git branch -a_](https://git-scm.com/docs/git-branch#Documentation/git-branch.txt--a)
- [_git branch -vv_](https://git-scm.com/docs/git-branch#Documentation/git-branch.txt--vv)
- [_git branch --set-upstream-to `<remote> <branch>`_](https://git-scm.com/docs/git-branch#Documentation/git-branch.txt---set-upstream-toltupstreamgt)
- [_git push -u `<remote> <branch>`_](https://git-scm.com/docs/git-push#Documentation/git-push.txt--u)

___________________

## Git Remote Branches 
> Lets take a quick look at [link](https://git-scm.com/book/en/v2/Git-Branching-Remote-Branches)
> Graph [link](https://devconnected.com/how-to-set-upstream-branch-on-git/) 

For this example we are going to work with two repositories:

> Repo1: git-upstream - https://github.com/JIMMYOnline/git-upstream

> Repo2: git-javascript - https://github.com/JIMMYOnline/git-javascript

# Steps

## 1. Clonar new repo
```
git clone https://github.com/JIMMYOnline/git-upstream.git
```
## 2. Listar remote repositories
```
git remote -v
```
_git remote [-v | --verbose]_ - Show remote url after name. [More info](https://git-scm.com/docs/git-remote)

> This should show at least the origin remote repo.

## 3. (Optional) Create alias to show commit logs
```
git config --global alias.glog "log --all --graph --oneline"
```
_Note: You can create it globally too_ [More info](https://git-scm.com/book/en/v2/Git-Basics-Git-Aliases)


## 4. Add new remote repository
```
git remote add js https://github.com/JIMMYOnline/javascript
```
_Note: `js` is the shortname for this new remote repository. The same as the `origin` refers to the base repo from where we initially cloned it this new shortname will refer to any other repos we want to link to._

[2.5 Git Basic - Working with Remotes. Adding Remote Repositories](https://git-scm.com/book/en/v2/Git-Basics-Working-with-Remotes)

## 5. Change upstream branch for a new branch
```
git checkout -b <new branch name>
git branch --set-upstream-to js/master
```
_This should give you an error since the remote tracking branch is not in our 
local computer yet. We need to fetch it_

Instead of:
```
git fetch origin master
```
we do:
```
git fetch js master
```
Now we check which branches we have.
```
git branch -a
```
We can now change the upstream branch.
```
git branch --set-upstream-to js/master
```
_Note: We can also run: `git push -u` and this would set the branch from where we are pushing to its own upstream branch `remote/origin/test` or `remote/js/test` for this case. This would be helpful in case we had just created a new branch and its remote tracking contrapart did not exist because the remote repository does not contain this new branch._
To verify that our change is effectively correct we can do:
```
git branch -vv
```
> Remember -vv displays the name of the upstream branch (if any) [More info](https://git-scm.com/docs/git-branch#Documentation/git-branch.txt--vv)

## 6. Push to new upstreamed branch
```
git push
```
_This will try to push our changes into the master branch in th javascript repository. However, since the branche origin diverge, it will warn you about it._
## 7. Error. Create a new branch and run git push instead of git push origin...

```
git checkout master
git checkout -b test2
```
> test2 does not exist in the remote repo

...do some changes and commit them...try to push

```
git push
```
_an error should be displayed sayig that no upstream is set up_
```
git branch -vv
```
Efectively there is no upsream branch set up, we need to create one. 
We can do so by pushing to the remote repository and branch we want like with `-u` flag.
```
git push -u origin test2
```
:bulb: [git push -u](https://git-scm.com/docs/git-push#Documentation/git-push.txt--u)

Links:

- [git remote](https://git-scm.com/docs/git-remote)
- [git log](https://git-scm.com/docs/git-log)
- [Git working with remotes](https://git-scm.com/book/en/v2/Git-Basics-Working-with-Remotes)
