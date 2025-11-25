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
git clone https://github.com/my-github-username/our-project
mkdir our-project
```
changing `my-github-username` and `our-project`

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

You're going to start by writing a story together. One of you should create a directory in the repo called `stories` and great a story in that directory called `story.md`. Type in the beginning of a story, either a work item or (if you're feeling creative) a fairy tale, and save it.

Enter `git status` again. Discuss with your partner what has changed.

To **stage** the change (sometimes referred to as "adding it to the **index**") run

```sh
git add *story.md*
```
Now run `git status` again and discuss what you see with your partner.

To commit the change and give it a description, run

```sh
git commit -m "added an initial story"
```
Note that if you forget the `-m` git will open a text editor for you to write your commit message. Try to avoid that.

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

So far we've been conflict avoidant, having each person pull changes before making their own. This time, have both of you make changes at the same time. The first one to push will be able to successfully; the second will get an error

```
(error message)
```

To resolve this, you'll need to do `git pull` to bring your partner's changes to your computer. Assuming your changes were made it different files, the merge will get trivial. You'll need to do `git commit` again, which create another commit on your computer that contains both changes. This "merge commit" has two parents: your previous commit and the commit that your partner created.

Once that is done, run `git push` to push the merged change. Your partner should to `git pull` to bring the merged change to their computer.

Look at `git log` again and discuss what you see. Note that this command has *many* options, for example, try

```sh
git log --oneline --graph
```

Finally, go to the repository on GitHub, click on the "Commits" button, and look at the results.

Repeat this in the other order, so your partner has to do a merge.

## Changes to the same file

Finally, both of you should make changes to the same file, and add, commit, and push the changes. Make changes to different areas of the file so they don't overlap. The resolution will be more complicated; follow advice it `git status` and in the changed file in VS Code.




