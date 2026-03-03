# Git class

## Set up Github repo

First, one of each pair (the one with less experience in git) should set up a new repository in GitHub for you both to work in, while the other watches and helps.

1. Go to https://github.com/
2. Click on **New** to create a new repository
3. Choose a name and add a brief description. Switch **Add README** to **On**, but leave other settings as is. Click on **Create repository**
4. You should now be on a page for the repository (if not: did you include a README?). Select **Settings** on the top bar and **Collaborators** on the left. Click on *Add People**. Enter the git username of your partner and click **Add to repository**.
5. Your partner should have an email invitation to join the repository. They should accept the invitation.


## Clone the repo locally

Both of you should clone the repo onto your local computer. You will both make changes locally and push to the remote repo on GitHub.

To do this, open a terminal on your computer and create and go to an appropriate directory under your home directory, e.g.
```sh
mkdir git-class
cd git-class
```
and clone the repository you created locally, using the URL of the repository, e.g.,
```sh
git clone https://github.com/*my-github-username*/*our-project*
cd *our-project*
```
changing `*my-github-username*` and `*our-project*`

Open up VS Code from that directory
```sh
code .
```

You'll be using the terminal quite a bit in this assignment. You can either use your existing window, or open a terminal within VSCode from the View -> Terminal menu.

## A first commit

Both of you should enter

```sh
git status
```
in the terminal. This is *the most frequent command* you should run; do this after every other command. Discuss what the output means with your partner.

You're going to start by writing a story together. One of you should create a directory in the repo called `stories` and creat a story in that directory called `story.md`. Type in the beginning of a story, either a work item or (if you're feeling creative) a fairy tale, and save it.

Enter `git status` again. Discuss with your partner what has changed.

To **stage** the change (sometimes referred to as "adding it to the **index**") run

```sh
git add story.md
```
Now run `git status` again and discuss what you see with your partner.

To commit the change and give it a description, run

```sh
git commit -m "added an initial story"
```
Note that if you forget the `-m` git will open a text editor you might not understand for you to write your commit message. Try to avoid that.

You ran `git status` and discussed it with your partner, right? I'm going to trust you to remember it from now on.

Once you've done that, run `git log` and discuss that with your partner as well.

## Pushing the changes

All this work is being done on the `main` branch (that's the first line in the response to `git status`). It's best practice to do all work on separate branches and merge them in later, but we'll ignore that in this lesson. Since you will generally be doing small changes that are isolated from other work and don't affect the code, it's generally safe to make changes directly to `main`, but note in some project workflows might require all changes happen in a feature branch.

To push the changes to the repository, do

```sh
git push
```

If you haven't used git before, it might ask you for a username; use your GitHub username. For a password, you'll need to create a PAT (personal access token).  Go back to the GitHub browser, click on your picture on the top right and go to **Settings**. Click on **Developer settings** (at the bottom) and then **Personal access tokens**, **Tokens (classic)** and click **Generate new token**. Click on **repo** to give it full repo permissions and have it generate the token. Copy the token into the terminal as the password.

You can save the token in a file for future use as needed.

**DO NOT ADD THIS FILE TO A GIT REPO UNDER ANY CIRCUMSTANCES**

Your partner should then do

```sh
git pull
```
to see your changes. Compare your results from `git status` and `git log`.

## Repeat

Your partner should then go through the same exercise, updating `story.md` (adding a new line to the story) the first person created, adding, committing, and pushing it, and having the other person pull the changes. Note that `git add` is the same command for adding a new file to a repo or changing an existing one.

Repeat this exercise a few more times each until you are both comfortable. As you do this:

 * Add another story file and push that as well. Note that you can have changes to multiple files in a single commit, and you can do multiple commits between pushes.
 * Add some Markdown tags. Lines starting with a hash (`#`) symbol show up as a large header; multiple hashes show up as smaller headers. Look at the files in the GitHub browser to confirm. If you're interested, read more about Markdown.
 * Try unstaging a change after you ran `git add` (as described in the output of `git status`). These messages are often useful.

## Merge conflicts

So far we've been conflict avoidant, having each person pull changes before making their own. This time, both of you make should make changes at the same time. The two of you should make changes to different files (to make it easier this first time), add, commit, and push them.

The first one to push will be able to successfully; the second will get an error.

To resolve this, you'll need to do `git pull` to bring your partner's changes to your computer. The first time you do that it might ask you about a how to reconcile divergent branches; you probably want the *merge* option (`git config pull.rebase false`) and then do `git pull` again.

Assuming your changes were made it different files, the merge will get trivial. Well, mostly: it will put you in an editor where you can edit the default message, but probably you just want to save and exit. If the editor is `vim` you'll want to hit the ESC key, then type `:x`, then the return key. As you might imagine, "how do i exit vim?" is a common question on many computer forums.

That will create a new commit that contains both changes. This "merge commit" has two parents: your previous commit and the commit that your partner created. Sometimes when doing a merge you'll have to do `git commit` explicitly, but since this is a simple merge it does it automatically.

Once that is done, run `git push` to push the merged change. Your partner should to `git pull` to bring the merged change to their computer.

Look at `git log` again and discuss what you see. Note that this command has *many* options, for example, try

```sh
git log --oneline --graph
```

Finally, go to the repository on GitHub, click on the "Commits" button, and look at the results.

Repeat this in the other order, so your partner has to do a merge.

## Changes to the same file

Next, both of you should make changes to the same file, and add, commit, and push the changes. For the first attempt, make them to different areas of the file, but have the other person push first so you can both practice. The experience should be the same, and it should merge the changes automatically.

Finally, make changes that overlap. As long as the changes are to different areas of the file, the `git pull` will give an error, something like

```Auto-merging README.md
CONFLICT (content): Merge conflict in story.md
Automatic merge failed; fix conflicts and then commit the result.
```
You looked at the result of `git status`, right? You'll need to fix the conflict manually and run `git add` on that file, and `git commit` again. If you're confused on this look at the message in `git status`. Git has added a bunch of stuff to the file showing the changes; if you open it up in VS Code it should help you with the merging.


## Optional: branches

If you have time, you should experiment with branches. To create a branch, do something like

`git branch feature-foo`

You can switch to that branch with

`git switch feature-foo`

and switch back to main with

`git switch main`

If you look at `git log` you'll notice they are both pointing to the same commit. If you add a new commit from one of those branches, it will affect one and not the other. Verify all this with `git status`, `git log`, and `git log --oneline --graph`.

If you push a branch for the first time you'll get a message like

```
fatal: The current branch foo has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin feature-foo

To have this happen automatically for branches without a tracking
upstream, see 'push.autoSetupRemote' in 'git help config'.
```

Do what it tells you to do.

To merge branch `feature-foo` into `main` do

```
git switch main
git merge feature-foo
```
This will move `main` to a new commit that contains all the changes that were made to `feature-foo`. Note you may have to resolve some conflicts.

Continue to explore with your partner, looking at how all of the commands affect the repos.
You can merge a branch into another with something



