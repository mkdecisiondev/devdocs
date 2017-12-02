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

## Learning resources

1. [Git book](https://git-scm.com/book/en/v2) (chapters 1-3, 5, 6-8)
1. [Feature branch workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow)
1. [Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)
1. [Rebase workflow](http://kensheedlo.com/essays/why-you-should-use-a-rebase-workflow/)
