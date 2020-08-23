This README contains the basic and advanced GIT commands.

AGENDA:-

1. Create your own Git repo, make commits to track changes.
2. Collaborate with others by pushing and pulling changes between repos, making pull requests, and merging them.
3. Learn about Git's branching model and how to work on multiple changes simultaneously.
4. Move commits around between branches, move branches around within repos.
5. Travel through time and change history in your repo.

rebase allows you to modify the history and rewrite to something that is closer to intended other than the actual commit.


To make a repo:- `git init cookbook` -> cookbook is repo name.

* git init creates a new, empty repo.
* Optional argument is the name of the directory to create, otherwise the repo will be created in the current directory.
* Creates a .git directory that stores all the repo information.

`ls .git` -> it is a hidden file. This .git directory is the location of commit history for git. Most of the time you don't need to touch the contents of .git directory but there is one very
useful file .git/config. Config is a pointtext file and it is in .ini format
you don't want to modify files info/, objects/ and refs/ directly because that's where git actually stores the git history.

GIT Config:-

`git config <key> [<value>]`

- git config allows you to read and write values to Git's config files.
- By default it uses .git/config
Use the --global flag to use ~/.gitconfig
- You'll need to set your name and email address:

`git config --global user.name "arjungoel"`
`git config --global user.email "arjungoel1995@gmail.com"`

The .gitconfig file is a global config file that lives in the home directory.
Everytime you make a commit git stores the information about who has made that commit.

`git status`

- git status tells you the status of the files in your repo: what is new, what has changed, what's been deleted.
- git status is always safe to run, and will never change or break anything in your repo and sometimes it gives suggestions what you want to do next.

`git add <file>`

- It just not add one file at a time, you can add directories as well. When you are going to add a directory it's going to recursively operate on every file in that directory.
- git add looks at the file what it is at that point of time and stages it to commit. If you do further modifications to that file after doing git add git will not automatically pick up all
those changes. When you are doing git add you are telling git I want to add this file as it is at that point in time to be deframed when I form a commit.

`git add .` -> It will add all the files.


`git commit`

- git commit creates a new commit based on the file you've marked using git add.
- A commit message is required: Git will open your text editor so you can write one.
- you can use the -m flag to provide a message on the command line.

`git commit -m "initial commit"`    
            OR
`git commit --message "initial commit"`

The above commands are same.


COMMITTING CHANGES:-

To commit a change to the repo, do the following:

- Edit files and save changes
- git add <files>
- git commit

Special case: to delete a file from the repo, use

`git rm <file>` - it is exactly like how you would use git add.

`git add` is the thing that says the upcoming commit should match the current state of my file system.

`git add -a` - This command is used to add all the changes.


`git log` -> displays a log of all the commits from most recent to least recent. Use the arrow keys to scroll, press "Q" to quit.

Viewing a commit:-

`git show <hash>` -> displays detailed information about a particular commit. The hash argument is optional, defaults to current commit. Use the arrow keys to scroll, press "Q" to quit. If you
don't provide any arguments to `git show` it's going to default to whatever the commit you are currently sitting on right now.

- The `git hash` is a number that is calculated based on the contents of the commit, the person who made the commit (name and email address) and the time that commit was made as well as the
parents that commit might have. It looks random but it is not. The chances of 2 different commits generating the same commit hash collides. We can use this unique string of letters and numbers(hash) as identifiers.

One nice thing about GIT in terms of references is that there are many different ways to reference the same commit and full complete hash is one way of doing so. You can also use a short 
commit hash (min. 4 characters). If many commits have the short commit hash as identical it won't give any information saying can't able to verify which actual commit is this.

`git diff` -> shows the changes you have made that haven't yet been committed.
- useful for checking to be sure that you have made all the changes you intend, and none of the ones you didn't.
- Use the --staged argument to view changes thtat you already added using `git add`.
- Use the arrow keys to scroll, press "Q" to quit.
* git diff is a great way of doing a quick sanity check to say have I made all the changes that I want to make and have I made any changes that I don't intend to make. By default `git diff` 
will show you the changes that you haven't yet added. It assumes any changes you have added is all verified.

If you want to see the things you have added:- `git diff --staged`
It will show you only the changes that have already been added for commit and not yet committted.

GIT, like most of the Version Control Systems (VCSs) treats the smallest level that you can modify as a line in a file. --staged is the changes that you have already run `git add` on. The termin git is the "staging area". When you run `git add` you are taking the changes in files and you are moving them into the staging area. And then when you run `git commit` you are taking the 
changes from the staging area and you are moving them into a commit.

`git reset HEAD <file>` -> This command is used to modify files and branches in git to point to different places. HEAD is the reference to the most recent commit.

If you don't like having to run `git add` thinking it is a double task there is a flag that you can pass to "git commit" which is `git commit -a` and that basically says take all of the 
changes that have changed on disk even the ones I haven't added and commit all of them, all in one go. But as a good practice this is not recommended.

`git config core.editor`

git checkout <hash> -> git checkout allows to view your project as it was at a particular commit (allows you to jump from one commit to another).
- You will get a big scary "detached HEAD" warning: ignore it for now.
- To get back to your most recent commit, use master instead of a hash like this: `git checkout master` (Do this before making any commits!)
When you are in a `detached HEAD` state any commits that you make you might not able to get back to them.



COLLABORATION (sharing commits across repositories):-

Centralized vs Distributed Version Control Systems:

* GIT is a distributed Version Control System that means there is no server no client every copy of a repository is a complete copy of the repository. Because GIT is a distributed version 
control system that means every repository can talk to any other repositories on the internet, other computers, or other repositories that lives on the same computer.

`git remote` -> It tells git this is a remote repository that I want to be able to interact with on a more frequent basis and I want to provide a nickname for this repository (short name). Youcan have as many remotes as you want. There is no limit on the number of remotes.

git remote add <name> <url> -> git remote creates short nicknames for URLs that point to other Git repos that you want to share commits with.
- Run git remote -v to list all the remotes that the repo knows about.
- Remotes are saved in the .git/config file: you can edit it, if you want.

- If you want to open the .git/config file in the Visual Code Editor:- code .git/config
- This file is in .ini format and ";" is used for comments. git does not use any comments by default. You also have .git/config in your home directory and that is the global git settings. The
  settings in that file will apply to all the repositories you have on your computer.
- Each remote has a different name so that you can differentiate them. However you could if you want to have 2 remotes that have 2 different names that both point to the same URL.


`git push` -> This command sends commits from your repo to another repo.
- Can specify a remote; if not, pushes to whatever remote is set as default.

`git push -u origin master` -> This is what GitHub tells you to run.
* -u origin sets the "origin" remote as the default remote. -u is the short form of --upstream.
* master is a branch, and it's the same thing we use to get back with the most recent commmit.

In addition to make commits on your local computer, GitHub allows you to make commits on GitHub as well. GitHub.com allows you to perform git operations through the web browser.

How do I get that online modification in my local machine?

`git pull` -> This command gets commit from another repo to your repo, and updates your files with those changes.
- Can specify a remote; if not, pulls from whatever remote is set as default.

When I run `git pull` that is actually doing two operations:-

git fetch + git merge

- `git fetch` is the command that downloads additional information from the remote that you specify. `git fetch` is what uses the internet in order to go out there and communicate with the
remote. "fetch" never changes the files on your computer, even if the commits say the file should change. All it does is get information and doesn't act on it.
- `git merge` is the part that acts on that information. So if fetch finds out that there are new commits, merge is going to update that files pulls those commits in and take advantage of
those commits.

`git remote <fetch>` -> This command downloads information from a remote, but does not change any files in your repo.
- Run automatically as part of `git pull`.
- It is the equivalent of saying: "Hey remote, tell me what's new since we last saw each-other!".

`git merge <remote>/master` -> This command combines the commits on a remote repo with the commits on your local repo.
- Creates a new commit that has multiple parents: called a "merge commit".
- every commit has a black pointer to its parent.
- When you run `git merge` you are pulling together other information and update your local repository based on that information.

`git clone <url>` -> This command makes a local copy of repo that is available at the given URL.
- The local copy is a full, complete repo, with all commits and history.
- local copy has a remote named origin, which is set to the original URL.
- The local copy is yours: you can change it however you want!

Taking an existing project and making your own changes is called "forking". It is easy to merge forks back together.

- every repository is under the control of permissions whosoever has made that repository.

PULL REQUESTS:-

1. Fork the repo, so you have control over your fork.
2. Make commits in your fork to change it however you want.
3. Contact the owner of the upstream repo, show your changes, ask the owner to pull your changes into upstream repo.

GitHub has a special interface for managing these requests, which they call Pull Requests.

When you run `git clone` it is just like an umbrella operation. It does `git init`, `git remote add origin`, `git pull` and downloads all the commits from other repos. So you have your own
repository but because you have done `git remote add` your copy has a reference to where it came from. You can make local clones on your local computers but you cannot send it to the
repository where it came from because you don't have permission for that.

Because git makes the authorship information based on whatever you specify in the .git/config file.

MERGING PULL REQUESTS:- 

* Can use the merge  button on a GitHub pull request.
* OR, do it manually with Git:
 - Add requester's fork as a remote
 - git fetch <remote>
 - git merge <remote>/master
 - git push
 - GitHub will automatically update the pull request.

:information_desk_person:

* `git pull` is `git fetch` followed by `git merge`

Because GIT is a distributed network and any repository can talk with any other repository people can make pull request not into just my fork of the code but also into anyone's fork of the
code, that's why it's not a centralized model it is a distributed model and anyone can talk with anyone and anyone can treat any repo as central server.

`git request-pull` -> This is backward in nature.


BRANCHING & HISTORY:- 

* GitHub treats pull requests as having two defined repositories and two defined branches inside of those repositories. If you push commits to your GitHub repository on the master branch when
  you already have a pull request those commits will get automatically added to existing pull requests which often you wants but sometimes isn't.


Structure of a commit:-

* A "commit" has two parts Content and Metadata and they are closely intwined together. The Content is the actual text that you put into the files. Metadata is things like the commit message,
the author, the date that the commit was made and so on. 
* One of the reasons of having Version Control Systems (VCSs) is to maintain not just the content but also to maintain the metadata.
* Most commits in your repositories have a parent pointer. Each commit points to its parent and that means that you can go backwards in time simply by following these chains of pointers.
That's why when we use `git checkout` to checkout an older commit and then run `git log` you are able to see the commits that are older than that but you couldn't see the commits that are 
more recent because these pointers only go in one direction. They only go from child to parent, never the other way around. So once you get to a particular commit you can only ever see its
parents.
* "MASTER" is the default name of your branch in the repository. A "Branch" is simply a linkedlist of commits that starts with a particular label and goes back in time all the way to the
initial commit of the repository. Incidentally the initial commit of the repository is the only commit that doesn't have the parent pointer.
* In GIT, a branch is implemented as a "label" that points to a commit and these labels are flexible and movable and infact they move very frequently. So if I want to add another commit to
this branch that label would automatically move to point that new commit. So a branch is just a label to a commit and all of its parents going back one at a time in a list. This also means
everytime we create a new commit, we also attach it to the master branch the label will automatically update and points to that new commit.
* "HEAD" is the reference to whatever commit you are currently sitting on in GIT. So when GIT warns you that you have a `detached HEAD` that means you are not attached to one of the branch
labels and when you make a new commit that commit will exist and the branch label will not update to point to it. As a result if you leave that commit behind by using `git checkout` to go some
place else there is nothing that points back to that commit and it will be very difficult to get back to it. Whereas if we have the handy "master" pointer we can always say just go back to 
master.
* "merge commits" can have more than one parent pointer. GIT actually treats merge commits as special. There are certain operations that are difficult to do with them because they have mutiple
parents.

`git branch` -> This command shows which branch exist in the repo, and which one you are currently attached to (if any). It allows you to see what your options are for jumping around through 
your history.
`git branch <branchname>` -> This command creates a new branch pointing to the commit you are currently sitting on.
`git branch -d <branchname>` -> This command deletes an existing branch from your local repo (not but from remotes!).
`git log --graph` - This command will show graph for all the commits.

* The purpose of the merge commit is to merge two or more branches of the code base into one.

`git checkout -b <branchname>` -> This command creates a new branch and immediately switches over to it.

`git branch --set-upstream` -> Every branch has its own "upstream" setting: the remote that the branch normally pulls from and pushes to, and the branch in that remote that it uses for those
operations.
- Normally the branch in the remotes has the same name as the local branch, but it doesn't have to. Different branches can default to different remotes. Actually each branch has its own 
upstream by default.


`The “fatal: refusing to merge unrelated histories” Git error` -> This error is resolved by toggling the allow-unrelated-histories switch. After a git pull or git merge command, add the 
following tag: `git pull origin master --allow-unrelated-histories`. 

For more info about this error refer to the link:- https://www.educative.io/edpresso/the-fatal-refusing-to-merge-unrelated-histories-git-error

`git cherry-pick <ref>` -> This command creates a new commit that is a copy of an existing commit that you reference: same changes, same files, same author.
- You can use a hash, branch name, or any other valid Git reference.
- This does not delete the referenced commit.

`git revert` -> This command does inverse of a cherry-pick.

`git reset <commit>` -> This command moves the branch poiner to make it point to whatever commit you want.
By default, it does not modify the files in your working tree, but use --hard to modify them.

Relative References:

* Use "~" after a reference to refer to its parent commit.
* You can use mutiple tildes (~~~~~) or define a number (~5).
* You can use HEAD to refer to the current commit.
* To refer to the parent of the current commit: HEAD~

- To remove the most recent commit from the current branch: `git reset --hard HEAD`. This command says reset the branch pointer that I am currently sitting at to point to the commit that is 
the parent of the current commit. reset can modify both branch pointers and files on disk. By default it will just do the branch pointer. If you pass --hard that says also update the files on the disk that they were exactly at another commit that I am pointing to.
- GIT has a built-in garbage collector that will clean up any commits that don't have any references pointing to them.


Flashback of "DETACHED HEAD":

- "HEAD" means the current commit.
- "detached" means not attached to a branch.
- "New" commits will also not be attached to a branch.
- Hard to find those commits again.

Solution: `git checkout -b <branchname>` to create a new branch for your commits.


CONFLICTS:-

What if you try to cherry-pick a change that has already happened on your branch? Or a change in a file that doesn't exist on your branch?

Resolving Conflicts: Git will alter the file to show conflicting lines. Edit the file to look the way you want in the code editor, then use `git add` to indicate that the conflict is resolved.

`git rebase <ref>` -> This command is used for changing the history. git rebase does a series of cherry-picks to recreate a branch on a different commit base, and moves the branch pointer to 
point the newly-created branch.
- Just like with cherry-pick, the old commits are not deleted.


CHANGING HISTORY:-

* Changing history is confusing for others.
* Never change history when other people might be using your branch, unless they know you're doing so.
* Never change history on master.
BEST PRACTICE:- only change history for commits that haven't yet been pushed to any remote. The best practice for changing history is only to do it in private. Once history has been made 
public to other people if you think other people might be using your branch then its confusing to them if you change the history of that branch.

* It is recommended to use Rebasing on feature branches that you don't except other people ever be looking at or using and you inform people after you modified history because they can always use `git reset` to alter their branch pointers to reflect the new altered history.
* The best thing to do is to only use rebase to modify commits before you have ever pushed them to GitHub or GitLab etc. After we do a rebase we do need to update the repository at certain 
other places because you are going to end up like a situation where your local repository is different from your remote repository. And if you try to do `git push` with this git is going to
tell you not to do something that you want to do. So in order to update this you have to write "-f" flag to git push or "--force".

`git push --force` is the one way of telling Git that yes I know the history has changed, I want you to update the remote to reflect the change history. force pushing on git can be dangerous
if you have changed history in a way that you don't want and you are loosing information and then you also tell to remote to loose that information as well but you can recover from it because
there are tools that allow you to undo or change a rebase but it is not so easy to do.

Interactive REBASE:-

`git rebase -i` 

Steps through commits and perform operations on them:
- Squash multiple commits together.
- Edit a commit to separate it into multiple smaller ones.
- Insert, delete and reorder commits in history.

You only have to do force push if you are changing history because force push changes a push from an append operation to an override operation and override is more dangerous than append.

Whether and how to rebase is an individual's or a team's perspective to debate on (PROS & CONS of doing so).

`git reflog` -> This command shows every commit you have touched recently, regardless of where that commit is in Git's history.
- Useful for recovering commits that you have lost track of. e.g. commits you have deleted through interactive rebasing.

A detached HEAD is a commit but doesn't have any branches pointing to it. So if you have a detached HEAD you can make a new branch and point it to that commit and it is no longer detached then


MISCELLANEOUS TOOLS:- 

`git tag` -> This command is like `git branch` but branches move and tags don't.
- useful for historical references: version 1.0 that shipped to customers, or was put on the production website.
- Tags can be lightweight or annotated. Lightweight tag is just a name that points to the commit just as with the branch. An Annotated Tag creates a tag object in Git and that tag object 
points to a commit but also allows you to type in notes.

Once you make a tag you cannot change it. Tags are designed to be fixed. There are operations to delete the tags but you have to be careful as everytime you do push or pull the tags go with itYou can have multiple tags that points to the same commit but you cannot edit a tag once it has been made public.

`git blame <file>` -> For every line, git blame will tell you who last changed the line.
- Useful for when something broke and you need to know who can fix it.
- To find out who was second-to-last to change a line, check out the commit before when the file changed, and run `git blame` again.

Git treats the atomic changeset of a unit as a line in a file. As you pass a file in the repository `git blame` will print out the entire file and for every line of the file it will tell you 
who is the last person to modify that file and what commit happened and when it had happened.

`git bisect` -> This command will help you find which commit introduced a breakage or a bug.
- Provide three things: a working commit, a broken commit, and a test to determine whether a commit is working or not.
- bisects uses binary search to quickly find the common things went from working to broken.

Commands for git bisect:-

1. `git bisect start`
2. `git checkout broken-commit`
3. `git bisect bad`
4. `git checkout working-commit`
5. `git bisect good`


Bisect is going to find a commit that is in between those 2 commits that you have specified and it is going to ask the developer is this commit GOOD or BAD? If it is broken then you chop-off
50% of the commits and it is going to test in the middle of the area that is unknown.

|-------------------------------------------------------|-------------------------------------------------------------------------|
Broken 							?								   Working


`git bisect run my_test.sh` 

- Even faster with an automated test.
- Return code 0 on success, return code 1 on failure.

Regex to check a commit message before it was done (To be checked)


HOOK SCRIPTS:-

`ls .git/hooks`

- Every Git repo has a "hooks" directory in the ".git" directory, with scripts that Git will run automatically.
- Names include: pre-commit, pre-push, pre-rebase, prepare-commit-message, etc.
- For more check pre-commit.com (YELP Framework)

git add by patch:-

`git add -p .`

* Situation: you are trying to add a new feature, but you discover you need to fix a bug to do so.
- Should be two separate commits, but code is tangled up.
- Use `git add -p` to craft commits one patch at a time, instead of by whole files.

`git gc` -> This command is used for Garbage collection.

DECK Link for ADVANCED GIT:- https://speakerdeck.com/singingwolfboy/advanced-git
DECK Link for DEEP DIVE GIT:- https://speakerdeck.com/singingwolfboy/get-started-with-git

