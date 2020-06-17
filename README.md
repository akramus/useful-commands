# useful-commands
## Git
Delete branches that no more exist on remote 
> git fetch -p && for branch in $(git branch -vv | grep ': gone]' | awk '{print $1}'); do git branch -D $branch; done


## netstat

To list the TCP ports that are being listened on
> sudo netstat -plnt

To list all listennig ports (tcp and upd)
> sudo netstat -ltup
