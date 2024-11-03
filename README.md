# Git Alias

![](https://i.imgur.com/waxVImv.png)
### [View all Roadmaps](https://github.com/nholuongut/all-roadmaps) &nbsp;&middot;&nbsp; [Best Practices](https://github.com/nholuongut/all-roadmaps/blob/main/public/best-practices/) &nbsp;&middot;&nbsp; [Questions](https://www.linkedin.com/in/nholuong/)
<br/>

This project provides many git alias commands that you can use as you like.

Contents:

* [Introduction](#introduction)
  * [What is Git Alias?](#what-is-git-alias)
  * [Where is the code?](#where-is-the-code)
  * [Why use this?](#why-use-this)
* [Install](#install)
* [Examples](#examples)
  * [Shortcut examples](#shortcut-examples)
  * [Accelerator examples](#accelerator-examples)
  * [Workflow examples](#workflow-examples)
  * [Optimization examples](#optimization-examples)
* [Customization](#customization)
  * [Status](#status)
  * [Log](#log)
  * [Format](#format)
* [Epilog](#epilog)
  * [See also](#see-also)
  * [To do](#to-do)
  * [Thanks](#thanks)


## Introduction


### What is Git Alias?

Git Alias is a collection of git version control shortcuts, functions, and commands:

  * Shortcuts such as `s` for `status`.

  * Improvements such as `optimize` to do a prune and repack with recommended settings.

  * Topic branch flows such as `topic-start` to create a new topic branch using master.

  * Visualizations such as `graphviz` to show logs and charts using third-party tools.


### Where is the code?

To see the complete code, view this file:

  * [gitalias.txt](gitalias.txt)


### Why use this?

We are creating this alias list because we type these commands many times daily, and we want the commands to be fast and also accurate.

We often work on teams, across many companies and organizations, and using multiple shells. We want to count on a set of aliases. For shorter commands, such as `s` for `status`, fast speed is nice. For longer commands, such as `repacker`, accurate settings are important.



## Install

Download the file [`gitalias.txt`](gitalias.txt):

```sh
curl -O https://raw.githubusercontent.com/nholuongut/git-alias/master/gitalias.txt
```

Typical usage for a typical user:

  * Save this file as a dot file in your home directory: `~/.gitalias.txt`

  * `git config --global include.path ~/.gitalias.txt` in terminal.  Or manually edit your git config dot file in your home directory such as `~/.gitconfig`, include the path to this file.

Example file `~/.gitconfig` with an entry to include the file `~/.gitalias.txt`:

```gitalias
[include]
  path = gitalias.txt
```


## Examples


### Shortcut examples

Letters:

```gitalias
a = add
b = branch
c = commit
```

Letters with options:

```gitalias
ap = add --patch
be = branch --edit-description
ci = commit --interactive
```


### Popular examples

Summarizing:

```gitalias
dd = diff --check --dirstat --find-copies --find-renames --histogram --color
ll = log --graph --topo-order --abbrev-commit --date=short --decorate --all --boundary --pretty=format:'%Cgreen%ad %Cred%h%Creset -%C(yellow)%d%Creset %s %Cblue[%cn]%Creset %Cblue%G?%Creset'
```

Committing:

```gitalias
cam = commit --amend --message
rbi = rebase --interactive @{upstream}
```


### Accelerator examples

Logging:

```gitalias
log-graph = log --graph --all  --decorate --oneline
log-my-week = !git log --author $(git config user.email) --since "1 week ago"
```

Searching:

```gitalias
grep-group =  grep --break --heading --line-number
grep-all = !"git rev-list --all | xargs git grep '$1'"
```


### Recovery examples

Backtracking:

```gitalias
uncommit = reset --soft HEAD~1
cleanout = !git clean -df && git checkout -- .
```

Preserving:

```gitalias
snapshot = !git stash push "snapshot: $(date)" && git stash apply "stash@{0}"
archive = !"f() { top=$(rev-parse --show-toplevel); cd $top; tar cvf $top.tar $top ; }; f"
```


### Coordination examples

Combining:

```gitalias
ours   = !"f() { git checkout --ours $@ && git add $@; }; f"
theirs = !"f() { git checkout --theirs $@ && git add $@; }; f"
```

Comparing:

```gitlias
incoming = !git remote update --prune; git log ..@{upstream}
outgoing = log @{upstream}..
```  


### Workflow examples

Synchronizing:

```gitalias
get = !git fetch --prune && git pull --rebase=preserve && git submodule update --init --recursive
put = !git commit --all && git push
```

Publishing:

```gitalias
publish = "!git push -u origin $(git branch-name)"
unpublish = "!git push origin :$(git branch-name)"
```

Branching:

```gitalias
topic-start = "!f(){ b=$1; git checkout master; git fetch; git rebase; git checkout -b "$b" master; };f"
topic-stop = "!f(){ b=$1; git checkout master; git branch -d "$b"; git push origin ":$b"; };f"
```


### Optimization examples

Naming:

```gitalias
top-name = rev-parse --show-toplevel
branch-name = rev-parse --abbrev-ref HEAD
upstream-name = !git for-each-ref --format='%(upstream:short)' $(git symbolic-ref -q HEAD)
```

Pluralizing:

```gitalias
branches = branch -a
stashes = stash list
tags = tag -n1 --list
```

Streamlining:

```gitalias
pruner = !git prune --expire=now; git reflog expire --expire-unreachable=now --rewrite --all
repacker = !git repack -a -d -f --depth=300 --window=300 --window-memory=1g
expunge = !"f() { git filter-branch --force --index-filter \"git rm --cached --ignore-unmatch $1\" --prune-empty --tag-name-filter cat -- --all }; f"
```


## Customization


If you want to use this file, and also want to change some of the items,
then one way is to use your git config file to include this gitalias file,
and also define your own alias items; a later alias takes precedence.

This section has examples that include this file, then add a customization.


### Status

To do your own custom terse status messages:

```gitalias
[include]
   path = .gitalias.txt
[alias]
  s = status -sb
```


### Log

To do your own custom log summaries:

```gitalias
[include]
   path = .gitalias.txt
[alias]
  l = log --graph --oneline
```

### Format

To do your own custom pretty formatting:

```gitalias
[include]
   path = .gitalias.txt
[format]
  pretty = "%H %ci %ce %ae %d %s"
```


## Epilog


### See also

More ideas for git improvements:

  * If you want to alias the git command, then use your shell, such as `alias g=git`.
  * If you want history views, see [git-recall](https://github.com/nholuongut/git-recall)
  * If you use `emacs` then see [Magit](https://magit.vc/)
  * If you use `node` then see [git-alias](https://www.npmjs.com/package/git-alias)

References:

  * [Git Basics - Git Aliases](https://git-scm.com/book/en/v2/Git-Basics-Git-Aliases)
  * [Git Basics - Tips and Tricks](https://git-scm.com/book/en/v1/Git-Basics-Tips-and-Tricks)


### To do

To do list in priority order:

* Create an alias that helps remove problem files, akin to `bfg`.

* Create installable packages such as for `apt`, `brew`, `dnf`.

* Create completion file for `bash`, `zsh`, etc.

* Create CI/CD pipeline.

* Create security checksum.

* Create announcement list.

* Request comments from git thought leaders.

* Create aliases for GitPrime metrics suggestions: unreviewed pull requests, new work percentage, legacy refactor percentage, active days, time to first comment, churn, time to resolve.


# 🚀 I'm are always open to your feedback.  Please contact as bellow information:
### [Contact ]
* [Name: Nho Luong]
* [Skype](luongutnho_skype)
* [Github](https://github.com/nholuongut/)
* [Linkedin](https://www.linkedin.com/in/nholuong/)
* [Email Address](luongutnho@hotmail.com)
* [PayPal.me](https://www.paypal.com/paypalme/nholuongut)

![](https://i.imgur.com/waxVImv.png)
![](Donate.png)
[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/nholuong)

# License
* Nho Luong (c). All Rights Reserved.🌟