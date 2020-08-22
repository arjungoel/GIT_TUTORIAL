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

ls .git -> it is a hidden file. This .git directory is the location of commit history for git. Most of the time you don't need to touch the contents of .git directory but there is one very
useful file .git/config. Config is a pointtext file and it is in .ini format
you don't want to modify files info/, objects/ and refs/ directly because that's where git actually stores the git history.

GIT Config:-

git config <key> [<value>]

- git config allows you to read and write values to Git's config files.
- By default it uses .git/config
Use the --global flag to use ~/.gitconfig
- You'll need to set your name and email address:

git config --global user.name "arjungoel"
git config --global user.email "arjungoel1995@gmail.com"

The .gitconfig file is a global config file that lives in the home directory.
Everytime you make a commit git stores the information about who has made that commit.

git status

- git status tells you the status of the files in your repo: what is new, what has changed, what's been deleted.
- git status is always safe to run, and will never change or break anything in your repo and sometimes it gives suggestions what you want to do next.

git add <file>

- It just not add one file at a time, you can add directories as well. When you are going to add a directory it's going to recursively operate on every file in that directory.
- git add looks at the file what it is at that point of time and stages it to commit. If you do further modifications to that file after doing git add git will not automatically pick up all
those changes. When you are doing git add you are telling git I want to add this file as it is at that point in time to be deframed when I form a commit.

git add . -> It will add all the files.


git commit

- git commit creates a new commit based on the file you've marked using git add.
- A commit message is required: Git will open your text editor so you can write one.
- you can use the -m flag to provide a message on the command line.

git commit -m "initial commit"    
            OR
git commit --message "initial commit"

The above commands are same.


COMMITTING CHANGES:-

To commit a change to the repo, do the following:

- Edit files and save changes
- git add <files>
- git commit

Special case: to delete a file from the repo, use

git rm <file> - it is exactly like how you would use git add.

git add is the thing that says the upcoming commit should match the current state of my file system.


git log -> displays a log of all the commits from most recent to least recent. Use the arrow keys to scroll, press "Q" to quit.

Viewing a commit:-

git show <hash> -> displays detailed information about a particular commit. The hash argument is optional, defaults to current commit. Use the arrow keys to scroll, press "Q" to quit. If you
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

git remote <fetch> -> This command downloads information from a remote, but does not change any files in your repo.
- Run automatically as part of `git pull`.
- It is the equivalent of saying: "Hey remote, tell me what's new since we last saw each-other!".

git merge <remote>/master -> This command combines the commits on a remote repo with the commits on your local repo.
- Creates a new commit that has multiple parents: called a "merge commit".
- every commit has a black pointer to its parent.
- When you run `git merge` you are pulling together other information and update your local repository based on that information.

git clone <url> -> This command makes a local copy of repo that is available at the given URL.
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
