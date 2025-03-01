Clone the remote repo `git clone <url>`

create a local branch and copy a remote branch `git checkout -b <branch_name> origin/<branch_name>`

merge `git merge <branch>`

history `git log`

one line history `git log --oneline --graph`

## Remote

add a remote`git remote add origin <url>`

view remote/s `git remote -v`

push the local branch to remote and set the remote tracking`git push --set-upstream origin my-branch

push all branches to remote `git push --all origin

set new remote `git remote remove origin && git remote rename new-origin origin`

## Upstream

`git push --set-upstream bitbucket --all` performs the following actions:

`git push` – Pushes local branches to the remote repository.
`--set-upstream` – Sets the specified remote (bitbucket in this case) as the upstream for all pushed branches.
bitbucket – The name of the remote repository (it must be configured with git remote add bitbucket <url>).
`--all` – Pushes all local branches to the bitbucket remote.

What happens when you run this command?

1. All your local branches will be pushed to the remote bitbucket repository.
2. Each pushed branch will be linked to its corresponding remote branch (git pull and git push will now work without specifying the remote and branch explicitly).
3. If some branches do not exist on the remote, they will be created.


## Git flow best practices
https://gist.github.com/calaway/ea880263b0c0495bb00ee877f001dc59


## Rebase

**Do not rebase commits that exist outside your repository and that people may have based work on.**

`git rebase <source branch> <target branch> `

## Squash
git -rebase -i HEAD~3 (commit from head which we want to squash)
git -rebase -i --root (squash into initial commit)





## Error when pushing the local repo to remote when remote has different history
git push
To github.com:yurabulany/devops-task-force.git
 ! [rejected]        develop -> develop (non-fast-forward)
error: failed to push some refs to 'github.com:yurabulany/devops-task-force.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. If you want to integrate the remote changes,
hint: use 'git pull' before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.





