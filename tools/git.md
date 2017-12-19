# Git

## Installation

1. Install [Git](https://git-scm.com/)
1. Configure Git
    1. `git config --global user.name <your name>`
	1. `git config --global user.email <your email>`
	    1. Use the same e-mail address associated with your GitHub account
	1. `git config --global gui.encoding utf-8`
	1. `git config --global core.autocrlf false`
	1. `git config --global core.safecrlf false`
	1. `git config --global pull.rebase true`
	1. `git config --global branch.autosetuprebase always`
1. GUIs (optional)
    1. (Windows) [TortoiseGit](https://tortoisegit.org/)
	1. (Windows) [Git Extensions](https://gitextensions.github.io/)
	1. (Mac, Windows) [Sourcetree](https://www.sourcetreeapp.com/)

## Git Gui

Git comes with a GUI in addition to the CLI. In Windows, you should be able to right-click a folder and choose "Git GUI Here" from the context menu to open it. In any OS, you can type `git gui` from the command line.

You can configure the tab size in Git Gui:

```shell
git config --global gui.tabsize 4
```

## Visual Studio Code

VS Code has built-in support for Git that is very useful.

## Git basics

Git stores the history of your code and simplifies collaboration, experimentation, and ensuring that you always have a stable copy of your code.

1. History: when you edit files, Git notices they have changed. It does not automatically track every change. When you have made a set of changes that you want Git to track, you commit those changes. Git's history is a tree of commits.
1. Branches: a new repository starts with a default branch named "master". We want to ensure master has completed, tested code, so if you start work on a new feature you create a new branch. When you create a new branch you get a copy of everything in master _at the time you create the branch_. Changes can continue happening in master while you make changes in your branch, but you will not automatically get those changes. When work in your branch is completed and tested it will be incorporated into master.
1. Rebasing: rebasing is the cleanest way of copying changes from one branch to another. When you create a new branch from master and need to copy new updates from master to your branch, you will rebase.

## Branching and rebasing with Git

Branching and rebasing will be a daily process, so it is very important that you understand it.

1. [Create a fork](https://guides.github.com/activities/forking/) of the repository you will be working with
1. Clone your fork locally
1. Create a new branch based off master: `git branch my-branch`
1. Do your work and make some commits in "my-branch"
1. When your work is done and you are ready to submit a [pull request](https://help.github.com/articles/about-pull-requests/), check if master has been updated
1. If master has been updated:
    1. check out master and pull
    1. check out "my-branch"
    1. `git rebase master`
1. Rebasing rewrites history, which can cause confusion if multiple people are collaborating on a branch. If you are not the only person working on the branch, be sure to coordinate with others every time you rebase. You will have to force push to send your updates to GitHub: `git push -f`
1. If there are conflicts during the rebase, you will have to resolve them - get help from a team member if you are not experienced with this process
1. Once you have rebased on master and pushed your branch to your GitHub fork, you can create a pull request

## Learning resources

1. [Git book](https://git-scm.com/book/en/v2) (chapters 1-3, 5, 6-8)
1. [Feature branch workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow)
1. [Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)
1. [Rebase workflow](http://kensheedlo.com/essays/why-you-should-use-a-rebase-workflow/)
