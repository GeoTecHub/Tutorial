# Basic commands for pushing the data

``` bash
git add .
git commit -m "massage"
git push
```

# Commands for replacing the data from other branch
1. Ensure You're on the GitMilin Branch:
First, make sure you are on your GitMilin branch.

``` bash

git checkout GitMilin

```

2. Reset the GitMilin Branch to Match thanuji:
You can reset your GitMilin branch to the latest commit of the thanuji branch. This will discard all local changes on GitMilin and make it identical to thanuji.

``` bash

git reset --hard origin/thanuji
```

3. Pull the Latest Changes from the thanuji Branch:
If you haven’t done this already, pull the latest changes from the thanuji branch.

``` bash

git pull origin thanuji
```
4. (Optional) Push the Reset Branch:
If you want to update the remote GitMilin branch to reflect the reset state, push the changes.

``` bash

git push --force origin GitMilin

```
What This Does:
The git reset --hard origin/thanuji command resets your current branch (GitMilin) to match the latest commit on the thanuji branch, effectively discarding all your local changes.
The --force option in the push command is necessary because a reset rewrites the commit history, and you'll need to force push to update the remote repository.
This approach will leave your GitMilin branch exactly as the thanuji branch without retaining any of your previous changes.
You can also with with gitDesktop versition 