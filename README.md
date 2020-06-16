# useful-commands
## Git
### delete branches that no more exist on remote 
> git fetch -p && for branch in $(git branch -vv | grep ': gone]' | awk '{print $1}'); do git branch -D $branch; done
