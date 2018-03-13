# gitcommands
## Helpful git commands

### Count number of code lines in git repository per user
As per http://www.commandlinefu.com/commands/view/3889/prints-per-line-contribution-per-author-for-a-git-repository

    git ls-files | xargs -n1 git blame --line-porcelain | sed -n 's/^author //p' | sort -f | uniq -ic | sort -nr
