---
title: 'Git'
excerpt: 'Git learnings, common commands or things I have needed to use.'
date: '2021-10-27'
author:
    name: Chris McKeown
tags: ['git', 'github']
---

<h1 align="center">GIT</h1>

---

# Git commands

-   `git clone <repo name>`
-   `git init . ` to initialise a
-   `git remote -v` to check git repo
-   `git remote set-url origin git@bitbucket.org:kiwi-codes/skillshare-mastering-pipelines.git` to set a new git repo
-   `git remote -v` to check update worked
-   `git branch -v` to check branch
-   `git fetch && git checkout <branch name>`
-   `git reset --hard origin/<branch-name>`
-   `git stash` to store changes without commiting allowing you to change branch
-   `git stash pop` to bring back stored changes from a `git stash`
-   `git branch <new-branch> <base-branch>` rename a change
-   `git branch -D <branchName>` - force delete

---

## Create project first then repo and connect the two

-   git remote add origin `https:/github.com/your-repo`
-   git add .
-   git commit -m "message"
-   git push --set-upstream origin master

---

# Git Remote

-   To check remote `git remote -v`
-   To remove reference to a github project run: `git remote remove origin`
-   To add origin: `git remote add origin <repo name>`

# React gottas when create a project

To create a github repo for a create-react-app do not add the below,
create a blank repo. Then follow the instructions to rename the branch
from master to main.

-   Readme
-   .gitignore
-   License

# Git Stash - Understanding Git Stashing

Git stashing is a feature that allows you to save changes in your working directory without committing them. It comes in handy when you're in the middle of working on a feature or bug fix and need to switch to a different branch or address an urgent task. Instead of committing incomplete changes or creating a separate branch, you can stash your changes and apply them later when you're ready to continue.

[Understanding Git Stashing](https://www.tutorialspoint.com/how-to-name-a-stash-and-retrieve-a-stash-by-name-in-git#:~:text=By%20default%2C%20when%20you%20use,a%20new%20stash%20is%20created.)

## Basic

-   Stash creation `git stash`
-   Viewing available stashes `git stash list`
-   Stash pop (revealing) `git stash pop`
-   Stash pop a specific item in the list array `git stash pop #` where # is the number in the list

## Naming

-   Creating a Named Stash `git stash save -m "my_stash_name"`
-   Retrieving a Stash by Name `git stash apply <my_stash_name>` which retains the stash in the list
    -   Dropping a Named Stash `git stash drop <stash_name>`
-   Retrieving a Stash by Name `git stash pop <my_stash_name>` which removes the stash from the list

# GITFU

## MERGING BRANCHES - REBASE OR MERGE ?

### MERGING MAIN BRANCH INTO FEATURE BRANCH

[merging-vs-rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)

1. Branch off main - ie: feature-1
2. Merge latest main into feature branch
3. Create PR - Merge into main

-   create unnecessary merge commits

### REBASING MAIN BRANCH INTO FEATURE BRANCH

1. Branch off main - ie: feature-1
2. Rebase main into feature branch
3. Create PR - Merge into main

-   clean !

Steps:

1. `git checkout <sourceBranch>`where development is the branch you are rebasing against
2. `git pull` to get latest, this is what you are rebasing against...
3. `git checkout <yourBranch>`
4. `git rebase development` where development is the branch you are rebasing against
5. `git push --force` --force is required

---

## SQUASH AND USEFUL COMMIT MESSAGES

Useful commit messages
Squash unnecessary commits or block of work into one commit.
Try to answer WHY a implementation detail was done in a certain way
git rebase -i [branch-name]

## GIT GRAPH

git log --graph --all

## FINDING ERRORS WITH GIT BISECT

git bisect start
git bisect bad [commit SHA]
git bisect good [commit SHA]
git bisect bad
git bisect good

## CLEANING UNUSED FILES YOUR BRANCH

git clean -fd

## RESET BRANCH TO WHAT IS IN REMOTE

git reset --hard origin/[branch name]

## (DANGER) USING THE FORCE

gpsup
git push --force-with-lease
will not override the remote branch
git push --force
overrides the remote branch

# Git Viewing git commit and PR history

Some basic commands:

-   [Git-Basics-Viewing-the-Commit-History](https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History)
-   Basic log command to see all raw non pretty output `git log`
-   To view last commits and their `git log --pretty=oneline --abbrev-commit --graph --decorate --all`
-   To view last commit and files modified `git log --stat`
-   To check files added `git diff --staged`
-   To check files committed `git diff ..master`

## Logging with a Graph form

-   The oneline and format option values are particularly useful with another log option called --graph. This option adds a nice little ASCII graph showing your branch and merge history: `git log --pretty=format:"%h %s" --graph`
-   `git log --pretty=format:"%h %s" --graph --name-only` shows a list of files modified

## Basic - How to check if there are remote changes before preforming a git pull

```
# fetch new commits from origin
$ git fetch

# check what are the differences and judge if safe to apply, `--name-only` to just get a list of files
$ git diff origin/master --name-only

# or use stat for output similar to output when `git pull` is used
$ git diff origin/master --stat

# actually merge the fetched commits
$ git pull
```

## Intermediate - List all who have worked on a repo and their commits

(git log)[https://git-scm.com/docs/git-log]

### Listing all those who have worked on a repo from the start

-   List all those that have worked on a repo `git shortlog -s -n -e --all` or `git shortlog --summary --numbered --email --all`
-   `git shortlog -s -n -e --all --no-merges` Added --no-merges to exclude statistics from merge commits.
-   `git shortlog --since=2.day -s -n -e --all --no-merges` Added --since=2.day to filter by X period.
-   add `--author="<authorname>"` to fitler by Author

### Listing all those who have worked on a repo within a given time period

-   start with fetch changes `git fetch origin`
-   Show changes by Author additions and subtractions for previous weeks `git log --since=1.weeks --numstat --pretty="%ae %H" | sed 's/@.*//g' | awk '{ if (NF == 1){ name = $1}; if(NF == 3) {plus[name] += $1; minus[name] += $2}} END { for (name in plus) {print name": +"plus[name]" -"minus[name]}}' | sort -k2 -gr`
-   Show changes by Author additions and subtractions for previous days `git log --since=5.days --numstat --pretty="%ae %H" | sed 's/@.*//g' | awk '{ if (NF == 1){ name = $1}; if(NF == 3) {plus[name] += $1; minus[name] += $2}} END { for (name in plus) {print name": +"plus[name]" -"minus[name]}}' | sort -k2 -gr`

-   list the change count in + and -`git log origin/develop --since=10.days --numstat --pretty="%ae %H" | sed 's/@.\*//g' | awk '{ if (NF == 1){ name = $1}; if(NF == 3) {plus[name] += $1; minus[name] += $2}} END { for (name in plus) {print name": +"plus[name]" -"minus[name]}}' | sort -k2 -gr`

-   need to check what the below did. In short they where not providing the output I wanted, either too much or too little.
    `git log --pretty="%an <%ae> %ad %d:%B" --date=short --all --since="5.day.ago" --full-history`
    `git log --pretty=format:"%ad:%an:%d:%B" --date=short --all --since=3.day.ago`
    `git log --graph --oneline --all --since=3.day.ago`

## Advanced -Using bash to list all file diff and those that have edited the files

I was after a command that could show me all the files changes on remote and list all those that had worked on each file and when the change was made. A deeper dive than just a `git diff origin/master --stat`

Found this useful to get a better picture. Does list all files that have been changed, but... does not list all the Authors. Once a git pull is run you can see the Authors for each file. Seems to only list Authors on those files that have changed that have already been pulled.

-   `git fetch`
-   then

```
bash -c '
  echo "----------------------------------------"
  echo "Active Committers (Last 5 days):"
  git log origin/develop --pretty="%an <%ae>" --since="5.day.ago" | sort -u
  git diff origin/develop --name-status |
  while IFS=$'\''\t'\'' read -r status file; do
    echo "----------------------------------------"
    echo "File: $file"
    commit_type="modify"
    if [[ "$status" == "A" ]]; then
      commit_type="add"
    elif [[ "$status" == "D" ]]; then
      commit_type="delete"
    fi
    echo "Type: $commit_type"
    git log --pretty="%an <%ae> %ad %d:%B" --date=short --since="5.day.ago" --all --follow --full-history -- "$file"
  done
'
```

-   `git pull` when happy

# Rolling back git commits

## Roll back one commit

-   `git log -n 2 --pretty="%H %s"` to list last 2 commit hash's, where:
    -   `-n 2` is the number. Remove to list all
    -   `%H` represents the full commit hash.
    -   `%s` represents the subject (first line) of the commit message.
-   `git reset --hard <commit_hash>` to roll back
