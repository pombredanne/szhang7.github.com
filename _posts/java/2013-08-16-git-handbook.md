---
layout: post
title: "Git Handbook"
description: "Git Handbook"
category: java
tags: [git, handbook, github]
---
{% include JB/setup %}

## Introduction
In software development, Git is a distributed version control and source code management `(SCM)` system with an emphasis on speed. Initially designed and developed by Linus Torvalds for Linux kernel development, Git has since been adopted by many other projects.

Every Git working directory is a full-fledged repository with complete history and full version tracking capabilities, not dependent on network access or a central server.

Git is free software distributed under the terms of the GNU General Public License version 2.

## Installation instructions

###Windows 2000/XP/Win7

###Unix-based Operating Systems(Linux, Solaris and Mac OS X)
    $ sudo apt-get install git git-core git-gui git-doc     # Install git

## Configuring git

###Configuring ssh key
    $ ssh-keygen -t rsa -C "your_email@example.com"
    # Create a new ssh key (press Enter while need to type a passphrase)

    $ sudo apt-get install xclip
    # Install xclip

    $ xclip -sel clip < ~/.ssh/id_rsa.pub
    # Copy the contents to clipboard, add to github account setting.

    $ ssh -T git@github.com
    # Showing 'Hi username!' means you've successfully authenticated.

###Set up git

####Username
    $ git config --global user.name "Your Name Here"
    # Set the default name for git to use when you commit

####Email
    $ git config --global user.email "your_email@example.com"
    # Set the email associated with your GitHub account

####Password caching
    $ git config --global credential.helper cache
    # Set git to use the credential memory cache

    $ git config --global credential.helper 'cache --timeout=3600'
    # Set the cache to timeout after 1 hour (setting is in seconds)
    
    Tip: You need git 1.7.10 or newer to use the credential helper

## Common commands
    $ git init
    $ git clone
    
    $ git add
    $ git status
    $ git diff
    $ git commit
    $ git reset
    $ git rm, mv
    $ git stash
    
    $ git branch
    $ git checkout
    $ git merge
    $ git log
    $ git tag
    
    $ git fetch, pull
    $ git push
    $ git remote
    
    $ git log
    $ git diff

###Getting and Creating Projects
In order to do anything in Git, you have to have a Git repository. This is where Git stores the data for the snapshots you are saving.

There are two main ways to get a Git repository. One way is to simply initialize a new one from an existing directory, such as a new project or a project new to source control. The second way is to clone one from a public Git repository, as you would do if you wanted a copy or wanted to work with someone on a project. We will cover both of these here.

####git init
Initializes a directory as a Git repository

    $ mkdir cbay
    $ cd cbay
    $ git init      #initialized empty Git repository in cbay/.git/

In a nutshell, you use `git init` to make an existing directory of content into a new Git repository. You can do this in any directory at any time, completely locally.

####git clone
Copy a git repository so you can add to it

    $ git clone [url]
    
    $ git cone git://github.com/szhang7/Hello-World.git

In a nutshell, you use `git clone` to get a local copy of a Git repository so you can look at it or start modifying it.

###Basic Snapshotting
Git is all about composing and saving snapshots of your project and then working with and comparing those snapshots. This section will explain the commands needed to compose and commit snapshots of your project.

####git add
Adds file contents to the staging area

    $ git status -s
    ?? README
    
    $ git add README
    
    $ git status -s
    A README
    
    $ vim README
    $ git status -s
    AM README
    
    $ git add .
    $ git add -A
    #add changes from all tracked and untracked files

In a nutshell, you run `git add` on a file when you want to include whatever changes you've made to it in your next commit snapshot.

####git status
View the status of your files in the working directory and staging area

    $ git status -s
    $ git status

In a nutshell, you run `git status` to see if anything has been modified and/or staged since your last commit so you can decide if you want to commit a new snapshot and what will be recorded in it.

####git diff
Shows diff of what is staged and what is modified but unstaged

    $ git diff              #show diff of unstaged changes
    $ git diff --cached     #show diff of staged changes
    $ git diff HEAD         #show diff of all staged or unstaged changes
    $ git diff --stat       #show summary of changes instead of a full diff

In a nutshell, you run `git diff` to see details of the `git status` command - how files have been modified or staged on a line by line basis.

####git commit
Records a snapshot of the staging area

    $ git commit -a         #automatically stage all tracked, modified files before the commit
    $ git commit -m 'changes to hello file'
    $ git commit -am 'changes to hello file'

In a nutshell, you run `git commit` to record the snapshot of your staged content.

####git reset
Undo changes and commits

    $ git reset HEAD        #undo the last commit and unstage the files
    $ git reset --soft      #undo the last commit
    $ git reset --hard      #undo the last commit, unstage files and undo any changes in the working directory

In a nutshell, you run `git reset HEAD` to undo the last commit, unstage files that you previously ran `git add` on and wish to not include in the next commit snapshot.

####git rm
Remove files from the staging area

    $ git rm file           #remove the file from the staging area entirely and also of your disk
    $ git rm file --cached  #remove the file from the staging area, but leave the file in the working directory.
    $ git mv                #git rm --cached orig; mv orig new; git add new

In a nutshell, you run `git rm` to remove files from being tracked in Git. It will also remove them from your working directory.

####git stash
Save changes made in the current index and working directory for later

    $ git stash             #add current changes to the stack
    $ git stash list        #view stashed currently on the stack
    $ git stash apply       #grab the item from the stash list and apply to current working directory
    $ git stash drop        #remove an item from the stash list

In a nutshell, run `git stash` to quickly save some changes that you're not ready to commit or save, but want to come back to while you work on something else.

###Branching and Merging 

####git branch
List, create and manage working contexts

    $ git branch                        #list your available branches
    $ git branch (branchname)           #create a new branch
    $ git branch -v                     #see the last commit on each branch
    $ git branch -d (branchname)        #delete a branch

In a nutshell, you use `git branch` to list your current branches, create new branches and delete unnecessary or already merged branches.

####git checkout
Switch to a new branch context

    $ git checkout -b (branchname)      #create and immediately switch to a branch
    $ git checkout master               #switch to branch 'master'
    
    $ git push (remote-name) :(branchname) #delete a branch
    $ git push remote-name --delete branchname
    # git push remote-name local-branch:remote-branch
    
####git merge
Merge a branch context into your current one

#####simple merges
    $ git branch removals
    $ git checkout -b removals
    $ git rm test.txt
    $ git commit -am 'removed test.txt'
    $ git checkout master
    $ git merge removals            #merge master with branch removals

#####more complex merges
    $ git branch change_class
    $ git checkout -b change_class
    $ vim hello.rb                  #modify hello.rb
    $ git commit -am 'changed the class name'
    
    $ git checkout master
    $ git mv hello.rb ruby.rb       #rename hello.rb-->ruby.rb
    $ vim ruby.rb                   #modify ruby.rb
    $ git diff                      #diff --git a/ruby.rb b/ruby.rb
    $ git commit -am 'added from ruby'
    $ git merge change_class

#####merge conflicts
    $ git branch fix_readme
    $ git checkout -b fix_readme
    $ vim README
    $ git commit -am 'fixed readme title'
    
    $ git checkout master
    $ vim README
    $ git commit -am 'fixed readme title differently'
    
    $ git merge fix_readme
    Auto-merging README
    CONFLICT (content): Merge conflict in README
    Automatic merge failed; fix conflicts and then commit the result.
    
    $ vim README        #here I'm fixing the conflict
    $ git diff          #show you both sides of the conflict and how you've resolved it as shown here.
    
    $ git status -s
    $ git add README
    $ git status 0s
    $ git commit

In a nutshell, you use `git merge` to combine another branch context into your current branch.

####git log
Show commit history of a branch

    $ git log                       #we'll see all the commit messages that we've done.
    $ git log --oneline             #see a more compact version of the same history.
    $ git log --oneline --graph     #see when the history was branched and merged
    
    $ git branch erlang
    $ git checkout -b erlang
    $ vim erlang_hw.erl
    $ git add erlang_hw.erl
    $ git commit -m 'added erlang'
    
    $ vim haskell.hs
    $ git add haskell.hs
    $ git commit -m 'added haskell'
    
    $ git checkout master
    $ vim ruby.rb
    $ git commit -am 'reverted to old class name'
    
    $ git log --oneline erlang
    
    # which commits are unique to a branch in comparison to another. 
    $ git log --oneline erlang ^master
    $ git log --oneline master ^erlang

    If we are interested in merging in the 'erlang' branch we want to see what commits are going to effect our snapshot when we do that merge. The way we tell Git that is by putting a ^ in front of the branch that we don't want to see.Note that the Windows command-line treats ^ as a special character, in which case you'll need to surround ^master in quotes. 

In a nutshell, you use `git log` to list out the commit history or list of changes people have made that lead to the snapshot at the tip of the branch.

####git tag
Tag a point in history as important

    $ git tag -a v1.0
    $ git log --oneline --decorate --graph
    
    $ git tag -a v0.9 558151a
    $ git log --oneline --decorate --graph
    
    $ git fetch origin --tags                   #fetch all tags from a remote repository
    $ git fetch <remote> tag <tag-name>         #want a single tag
    
    $ git push <remote> --tags                  #push tags to a remote repository

In a nutshell, you use `git tag` to mark a commit or point in your repo as important.

###Sharing and Updating Projects
Git doesn't have a central server like Subversion. All of the commands so far have been done locally, just updating a local database. To collaborate with other developers in Git, you have to put all that data on a server that the other developers have access to. The way Git does this is to synchronize your data with another repository. There is no real difference between a server and a client - a Git repository is a Git repository and you can synchronize between any two easily.

####git remote
List, add and delete remote repository aliases

    $ git remote            #list your remote aliases
    $ git remote -v         #see the actual URL for each alias
    
    $ git remote add        #add a new remote repository of your project
    #git remote add [alias] [url]
    
    $ git remote rm         #remove an existing remote alias
    #git remote rm [alias]
    
    $ git remote rename [old-alias] [new-alias] #rename remote aliases
    #git remote rename [old-alias] [new-alias]
    
    $ git remote set-url        #update an existing remoete URL
    $ git config remote.origin git://github.com/szhang7/HelloWorld.git

####git fetch
Download new branches and data from a remote repository

    $ git fetch [alias]         #synchronize you with another repo

In a nutshell, you run `git fetch [alias]` to synchronize your repository with a remote repository, fetching all the data it has that you do not into branch references locally for merging and whatnot.

####git pull
Fetch from a remote repo and try to merge into the current branch

    $ git pull
    #run a [git fetch] immediately followed by a [git merge]

####git push
Push your new branches and data to a remote repository

    $ git push [alias] [branch]         #make your [branch] the new [branch] on the [alias]
    $ git push github master            #push our 'master' branch to the new 'github' remote

#####Q&A
    $ git push github master
    To git@github.com:schacon/hw.git
     ! [rejected]        master -> master (non-fast-forward)
    error: failed to push some refs to 'git@github.com:schacon/hw.git'
    
    The solution:
    $ git fetch github
    $ git merge github/master
    #and then pushing again

In a nutshell, you run `git push [alias] [branch]` to update a remote repository with the changes you've made locally.

###Inspection and Comparison
In a nutshell you can use `git log` to find specific commits in your project history - by author, date, content or history. You can use `git diff` to compare two different points in your history - generally to see how two branches differ or what has changed from one version of your software to another.

####git log
Filter your commit history

    $ git log --author                  #look for only commits from a specific author
    $ git log --author=Linus --oneline -5
    #-[number] option will limit the results to the last [number] commits.
    
    $ git log --since --before          #filter commits by date committed
    $ git log --until --after
    $ git log --oneline --before={3.weeks.ago} --after={2010-04-18} --no-merges
    #--no-merges remove merge commits
    
    $ git log --grep                    #filter commits by commit message
    $ git log --grep=P4EDITOR --no-merges
    #commit messages including P4EDITOR
    
    $ git log --grep='p4 depo' --format="%h %an %s"
    #use --format option, so we can see who the author of each commit was.
    
    $ git log --grep="p4 depo" --format="%h %an %s" --author="Hausmann"
    #show all commits by Simmon OR commits with "p4 depo" in the message.
    
    $ git log --grep="p4 depo" --format="%h %an %s" --author="Hausmann" --all-match
    #show all commits by Simon and commits with "p4 depo" in the message.
    
    $ git log -S                    #filter by introduced diff
    $ git log -Suserformat_find_requirements
    #find which commits modified anything that looked like the function name 'userformat_find_requirements'
    
    $ git log -p                    #show patch introduced at each commit
    $ git log -p --no-merges -2
    #tells Git to put the patch after each commit
    
    $ git log --stat                #show diffstat of changes introduced at each commit
    $ git log --stat --no-merges -2
    #summarize the changes

####git diff
See the absolute changes between any two commit snapshots

    $ git diff [version]            #see what has changed since the last release
    $ git diff v0.9
    #see what has changed in our project since the v0.9 release
    
    $ git diff v0.9 --stat
    #summarize the changes
    
    $ git diff --stat master erlang         #wrong way
    
    $ git diff --stat 8d585ea erlang
    $ git diff --stat master...erlang       #recommended strongly 
    $ git diff --stat $(git merge-base master erlang) erlang
    #see what is on the "erlang" branch compared to the "master" branch.

In a nutshell, you can use `git diff` to see how a project has changed since a known point in the past or to see what unique work is in one branch since it diverged from another. Always use `git diff branchA...branchB` to inspect branchB relative to branchA to make things easier.

###git api思维导图
![1.jpg]({{ site.img_url }}/2013-08-16.png)

## REFERENCES
- [Set Up Git](https://help.github.com/articles/set-up-git)
- [Generating SSH Keys](https://help.github.com/articles/generating-ssh-keys)
- [Git Reference](http://gitref.org/index.html)
- [Git 常用命令](http://www.cnblogs.com/1-2-3/archive/2010/07/18/git-commands.html)

## APPENDIX A

###git commands
    function gm(){
    PARAM=$1
    # main menu
    clear
    echo "--------------------------------------------------------------------------------"
    time=`date +"%d%m%Y"`
    echo -e "USER:$USER\tHOST:$HOSTNAME\tDATE:$time"
    echo "--------------------------------------------------------------------------------"
    #Getting and Creating Projects
    echo -e "1.git init         -initializes a directory as a Git repository"
    echo -e "2.git clone        -copy a git repository so you can add to it"
    #Basic Snapshotting
    echo -e "3.git status       -view the status of your files and staging area"
    echo -e "4.git add          -adds file contents to the staging area"
    echo -e "5.git commit       -records a snapshot of the staging area"
    echo -e "6.git reset        -undo changes and commits"
    echo -e "7.git rm           -remove files from the staging area"
    echo -e "8.git stash        -save changes for later"
    #Branching and Merging
    echo -e "9.git branch       -list,create and manage working contexts"
    echo -e "c.git checkout     -switch to a new branch context"
    echo -e "m.git merge        -merge a branch context into your current one"
    echo -e "t.git tag          -tag a point in history as important"
    #Sharing and Updating Projects
    echo -e "r.git remote       -list,add and delete remote repository aliases"
    echo -e "f.git fetch,pull   -download new branches and data from a remote repo"
    echo -e "p.git push         -fetch from a remote and try to merge into the current"
    #Inspection and Comparison"
    echo -e "l.git log          -filter your commit history"
    echo -e "d.git diff        -show diff of what is staged and what is modified but unstaged"
    echo "--------------------------------------------------------------------------------"
    echo -n "Your choice [1,2,3,4,5,6,7,8,9,c,m,t,l,d]:"
    read -n1 choice
    echo 
    echo "--------------------------------------------------------------------------------"
    if [ "$choice" = "1" ]; then
        echo -e "1.git init"
        if [ -z "$PARAM" ]; then
            read -p "Please type a repository name:" PARAM
        fi
        if [ -n "$PARAM" ]; then
            if [ ! -d "$PARAM" ]; then
                mkdir "$PARAM"
            fi
            cd "$PARAM"
            git init
            cd ..
        else
            git init
        fi
    elif [ "$choice" = "2" ]; then
        echo -e "2.git clone"
        if [ -z "$PARAM" ]; then
            read -p "Please type URL:" PARAM
        fi
        if [ -n "$PARAM" ]; then
            git clone $PARAM
        else
            echo -e "[ERROR] URL is required!"
        fi
    elif [ "$choice" = "3" ]; then
        echo -e "3.git status"
        if [ "$PARAM" = "-s" ]; then
            git status -s
        else
            git status
        fi
    elif [ "$choice" = "4" ]; then
        echo -e "4.git add"
        git status -s
        if [ -z "$PARAM" ]; then
            read -p "Please type untracked files (. add all files):" PARAM
        fi
        if [ -n "$PARAM" ]; then
            git add $PARAM
        else
            echo -e "[ERROR] file is required!"
        fi
    elif [ "$choice" = "5" ]; then
        echo -e "5.git commit"
        git status -s
        if [ -z "$PARAM" ]; then
            read -p "Please type commit message:" PARAM
        fi
        if [ -n "$PARAM" ]; then
            #-a automatically stage all tracked, modified files before the commit
            git commit -am "$PARAM"
        else
            echo -e "[ERROR] file is required!"
        fi
    elif [ "$choice" = "6" ]; then
        clear
        echo -e "6.git reset"
    echo "--------------------------------------------------------------------------------"
        git status -s
        echo -e "1.git reset HEAD         -unstage files"
        echo -e "2.git reset --soft HEAD~ -undone the last commit"
        echo -e "3.git reset --hard HEAD  -undone the last commit, unstage files"
        read -n1 -p "Your choice:[1,2,3]:" response
        echo 
        if [ "$response" = "1" ]; then
            echo -e "[INFO] undo the last commit and unstage the files"
            git reset HEAD
        elif [ "$response" = "2" ]; then
            echo -e "[INFO] undo the last commit"
            git reset --soft HEAD~
        elif [ "$response" = "3" ]; then
            echo -e "[INFO] undo the last commit, unstage files AND undo any changes in the working directory"
            git reset --hard HEAD
        else
            echo -e "[WARNING] Invalid choice!"
        fi
    elif [ "$choice" = "7" ]; then
        echo -e "7.git rm"
        ls
        if [ -z "$PARAM" ]; then
            read -p "Please type files:" PARAM
        fi
        if [ -n "$PARAM" ]; then
            git rm "$PARAM"
        else
            echo -e "[ERROR] file is required!"
        fi
    elif [ "$choice" = "8" ]; then
        clear
        echo -e "8.git stash"
    echo "--------------------------------------------------------------------------------"
        echo -e "1.git stash        -add current changes to the stack"
        echo -e "2.git stash list   -view stashes currently on the stack"
        echo -e "3.git stash apply  -grab the item from the stash list and apply to current working directory"
        echo -e "4.git stash drop   -remove an item from the stash list"
        echo -e "5.git stash clear  -remove all of the stored items"
        read -n1 -p "Your choice:[1,2,3,4,5]:" response
        echo 
        if [ "$response" = "1" ]; then
            echo -e "[INFO] add current changes to the stack"
            git status -s
            git stash
            git status
        elif [ "$response" = "2" ]; then
            echo -e "[INFO] view stashes currently on the stack"
            git stash list
        elif [ "$response" = "3" ]; then
            echo -e "[INFO] grab the item from the stash list and apply to current working directory"
            git stash list
            git stash apply
        elif [ "$response" = "4" ]; then
            echo -e "[INFO] remove an item from the stash list"
            git stash list
            if [ -z "$PARAM" ]; then
                read -p "Please type list:" PARAM
            fi
            if [ -n "$PARAM" ]; then
                git stash drop "$PARAM"
            else
                #remove the last added stash item.
                git stash drop
            fi
        elif [ "$response" = "5" ]; then
            echo -e "[INFO] remove all of the stored items"
            git stash list
            git stash clear
        else
            echo -e "[WARNING] Invalid choice!"
        fi
    elif [ "$choice" = "9" ]; then
        clear
        echo -e "9.git branch"
    echo "--------------------------------------------------------------------------------"
        echo -e "1.git branch                       -list your available branches"
        echo -e "2.git branch branchname            -create a new branch"
        echo -e "3.git branch -v                    -see the last commit on each branch"
        echo -e "4.git branch -d branchname         -delete a branch"
        echo -e "5.git push remote-name :branchname -delete a remote branch"
        read -n1 -p "Your choice:[1,2,3,4,5]:" response
        echo 
        if [ "$response" = "1" ]; then
            echo -e "[INFO] list your available branches"
            git branch
        elif [ "$response" = "2" ]; then
            echo -e "[INFO] create a new branch"
            git branch
            read -p "Please type branchname:" PARAM
            git branch $PARAM
            git branch
        elif [ "$response" = "3" ]; then
            echo -e "[INFO] see the last commit on each branch"
            git branch -v
        elif [ "$response" = "4" ]; then
            echo -e "[INFO] delete a branch"
            git branch
            read -p "Please type branchname:" PARAM
            git branch -d $PARAM
            git branch
        elif [ "$response" = "5" ]; then
            echo -e "[INFO] delete a remote branch"
            git remote
            read -p "Please type branchname:" PARAM
            git push remote-name :$PARAM
        else
            echo -e "[WARNING] Invalid choice!"
        fi
    elif [ "$choice" = "c" ] || [ "$choice" = "C" ]; then
        echo -e "c.git checkout"
        git branch
        read -p "Please type branchname:" PARAM
        git checkout $PARAM
    elif [ "$choice" = "m" ] || [ "$choice" = "M" ]; then
        echo -e "m.git merge"
        git branch
        read -p "Please type branchname:" PARAM
        git merge $PARAM
    elif [ "$choice" = "t" ] || [ "$choice" = "T" ]; then
        echo -e "t.git tag"
        git log --oneline --decorate --graph
        read -p "Please type version (v1.0):" PARAM
        read -p "Please type a tag message:" PARAM1
        git tag -a $PARAM -m "$PARAM1"
        #tag a released commit 558151a
        #git tag -a v0.9 558151a
    elif [ "$choice" = "r" ] || [ "$choice" = "R" ]; then
        clear
        echo -e "r.git remote"
    echo "--------------------------------------------------------------------------------"
        echo -e "1.git remote           -list your remote aliases"
        echo -e "2.git remote add       -add a new remote repo"
        echo -e "3.git remote -v        -see the actual URL on each alias"
        echo -e "4.git remote rm        -removing an existing remote alias"
        echo -e "5.git remote rename [old-alias] [new-alias] -rename remote aliases"
        echo -e "6.git remote set-url   -update an existing remote URL"
        read -n1 -p "Your choice:[1,2,3,4,5,6]:" response
        echo 
        if [ "$response" = "1" ]; then
            echo -e "[INFO] list your remote aliases"
            git remote
        elif [ "$response" = "2" ]; then
            echo -e "[INFO] add a new remote repo of your project"
            git remote
            read -p "Please type alias:" PARAM
            read -p "Please type url:" PARAM1
            git remote add $PARAM $PARAM1
            git remote -v
        elif [ "$response" = "3" ]; then
            echo -e "[INFO] see the actual URL for each alias"
            git remote -v
        elif [ "$response" = "4" ]; then
            echo -e "[INFO] removing an existing remote alias"
            git remote -v
            read -p "Please type alias:" PARAM
            git remote rm $PARAM
            git remote -v
        elif [ "$response" = "5" ]; then
            echo -e "[INFO] rename remote aliases"
            git remote -v
            read -p "Please type old-alias:" PARAM
            read -p "Please type new-alias:" PARAM1
            git remote rename $PARAM $PARAM1
        elif [ "$response" = "6" ]; then
            echo -e "[INFO] update an existing remote URL"
            git remote -v
            read -p "Please type alias:" PARAM
            read -p "Please type url:" PARAM1
            git remote set-url $PARAM $PARAM1
            git remote -v
        else
            echo -e "[WARNING] Invalid choice!"
        fi
    elif [ "$choice" = "f" ] || [ "$choice" = "F" ]; then
        clear
        echo -e "f.get fetch, pull"
    echo "--------------------------------------------------------------------------------"
        echo -e "1.git fetch    -download new branches and data from a remote repo"
        echo -e "2.git merge    -merge a branch context into your current one"
        echo -e "3.git pull     -fetch from remote repo and merge into current branch"
        read -n1 -p "Your choice:[1,2,3]:" response
        echo 
        if [ "$response" = "1" ]; then
            echo -e "[INFO] download new branches and data from a remote repo"
            git remote -v
            read -p "Please type alias:" PARAM
            if [ -z "$PARAM" ]; then
                git fetch origin
            else
                git fetch $PARAM
            fi
        elif [ "$response" = "2" ]; then
            echo -e "[INFO] merge a branch context into your current one"
            git remote -v
            git branch -v
            read -p "Please type alias:" PARAM
            if [ -z "$PARAM" ]; then
                git log origin/master ^master
                git merge origin/master
            else
                read -p "Please type branch:" PARAM1
                git log $PARAM/$PARAM1 ^$PARAM1
                git merge $PARAM/$PARAM1
            fi
        elif [ "$response" = "3" ]; then
            echo -e "[INFO] fetch from a remote repo and try to merge into the current branch"
            git remote -v
            git branch -v
            read -p "Please type alias:" PARAM
            if [ -z "$PARAM" ]; then
                git pull origin master
            else
                read -p "Please type branch:" PARAM1
                git pull $PARAM $PARAM1
            fi
        else
            echo -e "[WARNING] Invalid choice!"
        fi
    elif [ "$choice" = "p" ] || [ "$choice" = "P" ]; then
        echo -e "p.git push [alias] [branch]"
        git remote -v
        git branch -v
        read -p "Please type alias:" PARAM
        if [ -z "$PARAM" ]; then
            git push origin master
        else
            read -p "Please type branch:" PARAM1
            git push $PARAM $PARAM1
        fi
    elif [ "$choice" = "l" ] || [ "$choice" = "L" ]; then
        clear
        echo -e "l.git log"
    echo "--------------------------------------------------------------------------------"
        echo -e "1.git log --author  -look for only commits from a specific author"
        echo -e "2.git log --since --before    -filter commits by date committed"
        echo -e "3.git log --grep    -filter commits by commit message"
        echo -e "4.git log -S        -filter by introduced diff"
        echo -e "5.git log -p        -show patch introduced at each commit"
        echo -e "6.git log --stat    -show diffstat of changes introduced at each commit"
        echo -e "7.git log --oneline -shorthand for --pretty=oneline --abbrev-commit"
        echo -e "8.git log --no-merges  -remove merge commits"
        echo -e "9.git log -[number]    -limit the results to the last [number] commits"
        echo -e "a.git log --all-match  -will logically AND all arguments"
        echo -e "f.git log --format     -format the results"
        read -n1 -p "Your choice:[1,2,3,4,5,6,7,8,9,a,f]:" response
        echo 
        if [ "$response" = "1" ]; then
            echo -e "[INFO] look for only commits from a specific author"
            read -p "Please type author:" PARAM
            if [ -z "$PARAM" ]; then
                git log --oneline -5
            else
                git log --author="$PARAM" --oneline
            fi
        elif [ "$response" = "2" ]; then
            echo -e "[INFO] filter commits by date committed"
            echo -e "--since --before"
            echo -e "--after --before"
            echo -e "--after --until"
            read -p "Please type since date:" PARAM
            read -p "Please type before date:" PARAM1
            if [ -z "$PARAM" ]; then
                if [ -z "$PARAM1" ]; then
                    git log --oneline -5
                else
                    git log --before={$PARAM1} --oneline
                fi
            else
                if [ -z "$PARAM1" ]; then
                    git log --after={$PARAM} --oneline
                else
                    git log --after={$PARAM} --before={$PARAM1} --oneline
                fi
            fi
        elif [ "$response" = "3" ]; then
            echo -e "[INFO] filter commits by commit message"
            read -p "Please type para:" PARAM
            if [ -z "$PARAM" ]; then
                git log --oneline -5
            else
                git log --grep="$PARAM" --oneline
            fi
        elif [ "$response" = "4" ]; then
            echo -e "[INFO] filter by introduced diff"
            read -p "Please type para:" PARAM
            if [ -z "$PARAM" ]; then
                git log --oneline -5
            else
                git log -S"$PARAM" --oneline
            fi
        elif [ "$response" = "5" ]; then
            echo -e "[INFO] show patch introduced at each commit"
            git log -p -2
        elif [ "$response" = "6" ]; then
            echo -e "[INFO] show diffstat of changes introduced at each commit"
            git log --stat -5
        elif [ "$response" = "7" ]; then
            echo -e "[INFO] shorthand for --pretty=oneline --abbrev-commit"
            git log --oneline -5
        elif [ "$response" = "8" ]; then
            echo -e "[INFO] remove merge commits"
            git log --no-merges -5
        elif [ "$response" = "9" ]; then
            echo -e "[INFO] limit the results to the last [number] commits"
            read -p "Please type number:" PARAM
            if [ -z "$PARAM" ]; then
                git log --oneline -5
            else
                git log -$PARAM --oneline
            fi
        elif [ "$response" = "a" ]; then
            echo -e "[INFO] will logically AND all arguments"
            read -p "Please type para:" PARAM
            read -p "Please type author:" PARAM1
            git log --grep="$PARAM" --author="$PARAM1" --format="%h %an %s"
        elif [ "$response" = "f" ]; then
            echo -e "[INFO] format the results"
            git log --format="%h %an %s" -5
        else
            echo -e "[WARNING] Invalid choice!"
        fi
    elif [ "$choice" = "d" ] || [ "$choice" = "D" ]; then
        clear
        echo -e "d.git diff"
    echo "--------------------------------------------------------------------------------"
        echo -e "1.git diff          -show diff of unstaged changes"
        echo -e "2.git diff --cached -show diff of staged changes"
        echo -e "3.git diff HEAD     -show diff of all staged or unstaged changes"
        echo -e "4.git diff --stat   -show summary of changes instead of a full diff"
        echo -e "5.git diff version  -see what changed since the last release"
        echo -e "6.git diff master...branchname  -see what is on branch compared to master"
        read -n1 -p "Your choice:[1,2,3,4,5,6]:" response
        echo 
        if [ "$response" = "1" ]; then
            echo -e "[INFO] show diff of unstaged changes"
            git status -s
            git diff
        elif [ "$response" = "2" ]; then
            echo -e "[INFO] show diff of staged changes"
            git status -s
            git diff --cached
        elif [ "$response" = "3" ]; then
            echo -e "[INFO] show diff of all staged or unstaged changes"
            git diff HEAD
        elif [ "$response" = "4" ]; then
            echo -e "[INFO] show summary of changes instead of a full diff"
            git status -s
            git diff --stat
            git diff --cached --stat
            git diff HEAD --stat
        elif [ "$response" = "5" ]; then
            echo -e "[INFO] see what changed since the last release"
            git log --oneline --decorate --all
            read -p "Please type tag:" PARAM
            if [ -n "$PARAM" ]; then
                git diff $PARAM --stat
                git diff $PARAM
            else
                echo -e "[WARNING] tag is required!"
            fi
        elif [ "$response" = "6" ]; then
            echo -e "[INFO] see what is on branch compared to master"
            git branch
            read -p "Please type branch:" PARAM
            if [ -n "$PARAM" ]; then
                #git diff master...$PARAM --stat
                git diff --stat $(git merge-base master $PARAM) $PARAM
            else
                echo -e "[WARNING] branch is required!"
            fi
            
        else
            echo -e "[WARNING] Invalid choice!"
        fi
    else
        echo -e "[WARNING] Invalid choice!"
    fi
    echo "--------------------------------------------------------------------------------"
    }
