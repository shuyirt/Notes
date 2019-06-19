# git 

- ##connecting to a remote repository

  `git remote add`



- ##`git clone`: clone a repo

  `git clone <url>`

- ## `git push`: uploading to a server 

  ### example 

  `git push origin master`

- ## `git pull`: getting changes from a server

  `git push origin master`

- ## `git branch`branching

  |                    |                               |
  | ------------------ | ----------------------------- |
  | create new branch  | `git branch <branch name>`    |
  | check out a branch | `git checkout <branch name>`  |
  | delete a branch    | `git branch -d <branch name>` |
  |                    |                               |
  |                    |                               |

- ## `git merge`: merge branch

  `git merge <branch A>`: merge branch A to current branch

- ## `git diff`: check the difference b/t commits

- ## `git`

## .gitignore file 

[Website for auto generating  .gitignore file]: https://www.gitignore.io

Rename Branch

```
git branch -m old_branch new_branch         # Rename branch in other branch  
or 
git branch -m new-name											# in the branch

git push origin :old_branch                 # Delete the old branch    

git push --set-upstream origin new_branch 
```

