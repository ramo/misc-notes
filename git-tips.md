# Commit History
## Different Git configurations for different projects
|Level|Command|
|------|-------|
|project|`git config user.name "John Doe" `|
|global|`git config --global user.name "John Doe"`|
|system|`git config --system user.name "John Doe" `|
- project overrides global and global overrides system.
- project configurations are local and not synced with remote.
### Reference
- https://stackoverflow.com/questions/8801729/is-it-possible-to-have-different-git-configuration-for-different-projects

## Replace commit/author name and email
- There are multiple ways to achieve this, but the below method solves it in single shot.
- Execute the below script in the Git project directory after editing the script with the old and correct name/emails.
```sh
#!/bin/sh

git filter-branch --env-filter '

OLD_EMAIL="your-old-email@example.com"
CORRECT_NAME="Your Correct Name"
CORRECT_EMAIL="your-correct-email@example.com"

if [ "$GIT_COMMITTER_EMAIL" = "$OLD_EMAIL" ]
then
export GIT_COMMITTER_NAME="$CORRECT_NAME"
export GIT_COMMITTER_EMAIL="$CORRECT_EMAIL"
fi
if [ "$GIT_AUTHOR_EMAIL" = "$OLD_EMAIL" ]
then
export GIT_AUTHOR_NAME="$CORRECT_NAME"
export GIT_AUTHOR_EMAIL="$CORRECT_EMAIL"
fi
' --tag-name-filter cat -- --branches --tags
```
- After successful execution of the script, verify the `git log` for the changes. 
- To make it permenant push the changes to remote by below command.
```
 git push --force --tags origin 'refs/heads/*'
```
### Reference
- https://stackoverflow.com/questions/3042437/how-to-change-the-commit-author-for-a-single-commit
- https://web.archive.org/web/20200823163529/https://docs.github.com/en/github/using-git/changing-author-info#changing-the-git-history-of-your-repository-using-a-script
