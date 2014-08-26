Git Guidelines and Best Practices
=================================

Date Created: 2014-08-26
Last Modified: 2014-08-26  

## Summary

This document describes the conventions and best practices applicable to IssueTrak project repositories. They are roughly based on [Fedora's Git Guidelines and Best Practices][fedoragit].

### Table of Contents

- [Git Daily Workflow](#git-daily-workflow)
- [Commit Messages](#commit-messages)
- [Pulling and pushing to master](#pulling-and-pushing-to-master)
- [Best Practices](#best-practices)
- [Terminology & Definitions](#terminology--definitions)


## Git Daily Workflow

IssueTrak does [Trunk Based Development (TBD)][tbd] (aka mainline development)
Assuming you have the appropriate repo cloned to your local workstation and have checked out the master branch:

### Visual Studio Workflow

1. From [Team Explorer][teamexplorer] home click 'Unsynched Commits' and then click the 'Sync' button
2. Click Team Explorer home button and then 'Branches'
3. Click the 'New Branch' dropdown and enter a branch name (make sure the second dropdown is 'master')
4. [DO YOUR WORK HERE]
5. From Team Explorer home click 'Changes'. Enter a commit message and click the 'Commit' button.
6. From Team Explorer home click 'Branches' and then click the 'Merge' dropdown button.
7. Select your branch from Step 3 as source and 'master' as the destination. Click 'Merge' button.
8. Click the 'Unsynched Commits' and then select 'master' for the branch. Click the 'Sync' button.

### Commandline Workflow

`git pull`
_pull all the changes from the remote repo_

`git checkout -b branch-name-here`
_create a new local branch for your bug/issue/story (i.e. git checkout -b devtrak15391)_

[DO YOUR WORK HERE]
_keep it in small chunks, the smaller your commits the better, in case things go wrong_

`git add .`
_add any new files you've created_

`git status` _and/or_ `git diff`
_see the changes you're going to commit_ 

`git commit -m "DevTrak #123: Good message here"`
_start your message with the correct issue number (if appropriate)_

`git checkout master`
_switch back to the master branch when the feature/fix is done, your tests pass right?_

`git merge branch-name-here`
_update the master branch with all of your changes_

`git push`
_send your changes to the remote repo (i.e. TFS)_

## Commit Messages

Commit messages should follow the guidelines described in detail in [Tim Pope's "A Note About Git Commit Messages"][tpope].

**Note:** _Visual Studio 2012 & 2013 just hit the enter key in the commit message textbox to add more lines._

 In summary:

- First line: DevTrak or Support Issue ID, followed by a brief description (~50 characters)
- Second line: blank
- Following lines: more detailed description, line-wrapped at 72 characters. May contain multiple paragraphs, separated by blank lines. Link to the Issue, if applicable.

Use the present tense when writing messages, i.e. "Fix bug, apply patch", not "Fixed bug, applied patch."

**Four sample commit messages**

* linked to a DevTrak issue:

		DevTrak #15391: Fix bug, update date formats
	
		Fix for the following bug: IssueTrak will not submit an issue when 
		certain date formats are set. These include: dd-mmm-yyyy, dd-mmm-yy, 
		dd/mm/yyy and dd/mm/yy.

		http://devtrak/CSIssue_View.asp?IssueNbr=15391

* linked to a Support issue:

		Support #78494: Add SQL code to insert missing records

		Fix for the following bug: Duplicate SLAs are being generated for 
		issues, which is causing an error with the API.

		https://support.issuetrak.com/CSIssue_View.asp?IssueNbr=78494

* linked to a TFS issue:

		Implement custom swagger comment attribute

		Story for the following item: Add the ability to annotate API
		methods with attributes which will be shown in the Swagger
		API documentation.

		Related Work Items: #500

* general issue:

		Create .gitattributes file to normalize line feeds

		Create .gitattributes file requesting all text files normalised to LF.
		Will be ignored by git versions < 1.7.2

		See https://wiki.duraspace.org/display/FCREPO/Git+Guidelines+and+Best+Practices
		for more information.



## Best Practices

* Bugs are fixed on the main branch and merged or 'cherry-picked' into the appropriate release branch.
* Always ensure all unit tests are passing before pushing your code to remote.

Two things you should never do in git:
- NEVER force a push
	- If you find yourself in a situation where your changes can't be pushed upstream, something is wrong. Contact another IssueTrak developer for help tracking down the problem.
- NEVER rebase a branch that you pushed, or that you pulled from another person. 
	- Rebasing published branches can lead to duplicate commits in the shared repository

## Terminology & Definitions

|Term         						|Definition     													|
|-----------------------------------|-------------------------------------------------------------------|
|master       						| this is the main code branch, equivalent to trunk in Subversion. Branches are generally created off of master.|
|origin		  						| the default remote repository that all your branches are pull'ed from and push'ed to. This is defined when you execute the initial git clone command.|
|unpublished vs. published branches | an unpublished branch is a branch that only exists on your local workstation, in your local repository. Nobody but you knows that branch exists. A published branch is one that has been push'ed up to github, and is available for other developers to checkout and work on.|
|fast-forward						| the process of bringing a branch up-to-date with another branch, by fast-forwarding the commits in one branch onto the other.|
|rebase								| the process by which you cut off the changes made in your local branch, and graft them onto the end of another branch.|




[fedoragit]: https://wiki.duraspace.org/display/FCREPO/Git+Guidelines+and+Best+Practices
[tpope]: http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html
[sourcetree]: http://www.sourcetreeapp.com/
[gitforwin]: https://windows.github.com/
[simplegit]: http://rogerdudler.github.io/git-guide/
[tbd]: http://paulhammant.com/2013/04/05/what-is-trunk-based-development/
[teamexplorer]: http://msdn.microsoft.com/en-us/library/hh500420.aspx