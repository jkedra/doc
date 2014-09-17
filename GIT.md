## GIT Aliases ##

    git config --global alias.co checkout
    git config --global alias.br branch
    git config --global alias.ci commit
    git config --global alias.st status
    git config --global alias.unstage 'reset HEAD --'
    git config --global alias.last 'log -1 HEAD'
    git config --global alias.alias 'config --global --get-regexp alias.\*'
    git config --global alias.logf 'log --name-only'
    git config --global alias.logg 'log --pretty=format:"%h %s" --graph'
    git config --global alias.diffl 'diff HEAD~'
