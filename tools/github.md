# GitHub

1. If you don't already have one, create a [GitHub account](https://github.com/)
1. Enable [two-factor authentication](https://github.com/blog/1614-two-factor-authentication)
1. GitHub's appearance can easily be customized with [Sylish](https://chrome.google.com/webstore/detail/stylish-custom-themes-for/fjnbnpbmkenffdnngjfgmeleoegfcffe). If you just want to change tab width from 8 to 4, you may find [this extension](https://chrome.google.com/webstore/detail/tab-size-on-github/ofjbgncegkdemndciafljngjbdpfmbkn) convenient. With Stylish more customization is easy. You can create a new style and use the following to customize to your preference:
```css
/* affects source code blocks */
.blob-code-inner,
.highlight {
	font-size: 16px;
	tab-size: 4;
}

/* affects all container blocks */
.container {
	width: 1200px;
}
```

## GitHub workflow

Using GitHub will be a daily process so it is very important that you understand it.

1. Clone the main repository, e.g. `https://github.com/mkdecisiondev/project.git`
	1. This step should create a remote named `origin` that points to `https://github.com/mkdecisiondev/project.git`
1. [Create a fork](https://guides.github.com/activities/forking/) of the repository you will be working with
1. Add a remote for your fork: `git remote add <GitHub username> https://github.com/<GitHub username>/project.git>`
1. Create a new branch based off master: `git checkout -b my-branch`
1. Do your work and make some commits in "my-branch"
1. When your work is done and you are ready to submit a [pull request](https://help.github.com/articles/about-pull-requests/), check if master has been updated
1. If master has been updated you will need to rebase those changes into your branch:
    1. `git checkout master`
	1. `git pull origin master`
    1. `git checkout my-branch`
    1. `git rebase master`
1. Rebasing rewrites history, which can cause confusion if multiple people are collaborating on a branch. If you are not the only person working on the branch, be sure to coordinate with others every time you rebase. You will have to force push to send your updates to GitHub: `git push -f`
1. If there are conflicts during the rebase, you will have to resolve them - get help from a team member if you are not experienced with this process
1. Once you have rebased on master and pushed your branch to your GitHub fork, you can create a pull request

### Important concepts

* `remote`: a URL from which a repository can be fetched.
* `origin`: this is the default name for the primary remote for a repository. It should point to the repository under the "mkdecisiondev" organization.
* `fork`: a copy of a repository on GitHub. A fork is a GitHub feature, not a Git concept. Typically you will only have read access to repositories on GitHub.
	By creating a fork, you have a copy of the repository on GitHub that you have write access to which enables you to create pull requests to the main repository.
	There is no automatic synchronization between the main repo and your fork. To update master, or any other branch on your fork you have to push from your local repo.
* `rebase`: a Git procedure that inserts commits into history.

### Naming remotes

* `origin`: this should always be the primary team repository under the "mkdecisiondev" organization
* `upstream`: don't use this naming scheme
* `<username>`: for remotes pointing to your fork, or other team member's forks, name the remote the same as their GitHub user name

### Managing remotes

A good GUI like TortoiseGit makes this easy. If you prefer the CLI then learn how to use [`git remote`](https://git-scm.com/book/en/v2/Git-Basics-Working-with-Remotes). If you accidentally cloned from a fork, you will end up with `origin` pointing to the fork. Rename that remote and create a new `origin` that points to `mkdecisiondev`.

 ### Rebase example

 At the time you create the branch `new-feature` the history may look like this:
 ```
 Branch: master
 A -> B -> C

 Branch: new-feature
 A -> B -> C -> D
 ```

 While work is being done in `new-feature`, updates are also made to `master`:
 ```
 Branch: master
A -> B -> C -> E

Branch: new-feature
A -> B -> C -> D
```

To avoid creating merge commits, `new-feature` can be rebased on `master`:
```
Branch: new-feature
A -> B -> C -> E -> D
```

Branches should ideally be short-lived and introduce a compact set of changes. If you are working in a branch for days or weeks, you should regularly check if you need to
rebase on master. Waiting to merge a large set of changes will be complicated.
