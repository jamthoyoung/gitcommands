# gitcommands
## Helpful git commands

### List globally installed packages

    npm list -g --depth=0

### Count number of code lines in git repository per user
As per http://www.commandlinefu.com/commands/view/3889/prints-per-line-contribution-per-author-for-a-git-repository

    git ls-files | xargs -n1 git blame --line-porcelain | sed -n 's/^author //p' | sort -f | uniq -ic | sort -nr

### Fix committer name and email
As per https://stackoverflow.com/questions/750172/change-the-author-and-committer-name-and-e-mail-of-multiple-commits-in-git

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

### Logging commands
List file names

     git log --name-only

### Restoring files
Checking difference of a file or folder

     git diff --name-only HEAD GOOD_SHA
     git diff HEAD GOOD_SHA -- the_path

Then fix it

     git checkout GOOD_SHA -- file1/to/restore file2/to/restore

Partial checkout to interactivly reset each change in a file back to HEAD

     git checkout -p myfile

Or from previous commit

     git checkout -p GOOD_SHA myfile

Overwrite file with another branch HEAD

     git checkout myotherbranch myfile
