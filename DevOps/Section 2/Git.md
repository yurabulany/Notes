Clone the remote repo `git clone <url>`

create a local branch and copy a remote branch `git checkout -b <branch_name> origin/<branch_name>`

merge `git merge <branch>`

history `git log`

## Remote

add a remote`git remote add origin <url>`
view remote/s `git remote -v`

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