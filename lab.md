# Introductory git assignment

This is a paired assignment. Ideally, do it in person, side by side, but it can also be done remotely if needed, with each person sharing their screen.

Communicate with your partner as you work: talk about what you are doing, what you expect to happen, and what actually happens. If you get stuck, reach out to the instructor.

At minimum, you should make it to the beginning of the **Merge conflicts** section, but try to complete as much as you can.

Feel free to experiment. You are very unlikely to break anything in a serious way.

## Learning objectives

You should already have watched the video that goes with this lab. It is not strictly required, but it should help you understand some of the key concepts around git and version control.

After watching the video and completing this lab, you should be able to:

- Explain the purpose of git, its role in collaborative development, and how it relates to GitHub
- Define basic git concepts, including **repository**, **commit**, **index**, **merge**, and **branch**
- Use git on the command line to:
  - `clone` a repository
  - `add` and modify files
  - `commit` and `push` changes
  - understand the `status` and history of a repository
  - resolve simple `merge` conflicts
- Collaborate effectively using git with another person

After the lab, review these objectives and check in with the instructor if you still have questions.

## Set up a GitHub repo

First, one person in the pair (ideally the one with less git experience) should create a new repository in GitHub for both of you to use, while the other person watches and helps.

1. Go to `https://github.com/`
2. Log in if needed, or create an account
3. Click **New** to create a new repository
4. Choose a name and add a brief description
5. Turn **Add README** to **On**
6. Leave the other settings as they are, then click **Create repository**

You should now be on the repository page.

Next, invite your partner:

1. Click **Settings** near the top of the repository page
2. Click **Collaborators** (or **Collaborators and teams**) on the left
3. Click **Add people**
4. Enter your partner's GitHub username
5. Click **Add to repository**

Your partner should receive an invitation and accept it.

## Clone the repo locally

Both of you should now clone the repository onto your own computer.

Open a terminal and make a folder for this class somewhere under your home directory, for example:

```sh
mkdir git-class
cd git-class
```

Now clone the repository:

```sh
git clone https://github.com/my-github-username/our-project
cd our-project
```

Replace `my-github-username` and `our-project` with the actual values for your repository.

Now open the folder in VS Code:

```sh
code .
```

If `code .` does not work, just open VS Code normally and use **File → Open Folder** to open the repository folder.

You will be using the terminal a lot in this assignment. You can keep using your current terminal window, or open a terminal inside VS Code with **View → Terminal**.

## A first commit

Both of you should run:

```sh
git status
```

This is one of the most important git commands. You should get in the habit of running it frequently.

Discuss with your partner what the output means.

You are going to start by writing a story together.

One of you should:

1. Create a directory in the repo called `stories`
2. Create a file in that directory called `story.md`
3. Type the beginning of a story into that file and save it

This can be a work item, or, if you are feeling creative, a fairy tale.

Now run:

```sh
git status
```

Discuss with your partner what changed.

To **stage** the file (sometimes called “adding it to the **index**”), run:

```sh
git add stories/story.md
```

Now run `git status` again and discuss what you see.

To commit the change and give it a description, run:

```sh
git commit -m "Add initial story"
```

If you forget the `-m`, git will open a text editor so you can write the commit message there. That is fine, but it may be confusing the first time.

Now run:

```sh
git status
git log
```

Discuss both outputs with your partner.

## Pushing the changes

All of this work is happening on the `main` branch. You can see that in the output of `git status`.

For this lab, we are working directly on `main` to keep things simple. In many real projects, people use feature branches and pull requests instead.

Now push your change to GitHub:

```sh
git push
```

The first time you do this, git may ask you to sign in to GitHub. On many Windows setups, this should open a browser window and let you sign in there.

If it asks for credentials in the terminal and you are unsure what to do, ask the instructor for help rather than guessing.

Once the push succeeds, your partner should run:

```sh
git pull
```

They should now be able to see your changes.

Compare your results from:

```sh
git status
git log
```

## Repeat

Now switch roles.

Your partner should update `stories/story.md` by adding another line to the story, then:

- `git add`
- `git commit`
- `git push`

The other partner should then run `git pull`.

Repeat this process a few more times until both of you are comfortable.

As you do this, try the following:

- Add another story file and push that as well
- Notice that one commit can include changes to more than one file
- Notice that you can make multiple commits before pushing
- Add some Markdown formatting:
  - A line starting with `#` becomes a large heading
  - Lines starting with `##` become smaller headings
- Look at the files in the GitHub browser to confirm what Markdown looks like there
- Try **unstaging** a change after running `git add` by following the instructions shown in `git status`

The messages in `git status` are often very helpful.

## Merge conflicts

So far, you have mostly been avoiding conflicts by pulling before making new changes.

This time, both of you should make changes at the same time.

For the first round, make changes to **different files** so it is easier.

Each of you should:

1. Edit a file
2. Run `git add`
3. Run `git commit`
4. Run `git push`

The first person to push will probably succeed.

The second person will probably get an error saying that their branch is behind the remote one.

When that second person runs `git pull`, git may stop and ask them to choose how to reconcile the divergent branches. This happens because both people have made new commits, so git wants you to say whether future pulls should usually make a merge commit or instead rebase local commits.

For this lab, set git to use merging on pull:

```sh
git config pull.rebase false
git pull
```

The config command tells git that when `git pull` has to combine local and remote work, it should do that by **merging** rather than **rebasing**. That is simpler for this lab, because it preserves the history in a way that is easier to see and discuss.

If your changes were in different files, the merge should be simple. Git may open an editor for a merge commit message. Usually you can just save and exit.

If the editor is `vim`, press:

1. `Esc`
2. type `:x`
3. press Enter

This creates a new **merge commit** that combines both lines of work.

Now run:

```sh
git push
```

Your partner should then run:

```sh
git pull
```

Look at the history again and discuss what you see:

```sh
git log
git log --oneline --graph
```

Then go to the repository on GitHub, click the **Commits** link, and compare what you see there.

Repeat the exercise in the other order so that the other partner has to do the merge.

## Changes to the same file

Next, both of you should make changes to the **same file**.

### First: different parts of the same file

For the first attempt, make changes to **different parts** of the file.

Then have one person push first. The second person should again run:

```sh
git pull
```

Because the changes are in different parts of the file, git will usually merge them automatically.

### Then: overlapping changes

Now both of you should edit the **same part** of the file so that the changes overlap.

Again, have one person push first. When the second person runs:

```sh
git pull
```

git should report a conflict, something like:

```text
Auto-merging story.md
CONFLICT (content): Merge conflict in story.md
Automatic merge failed; fix conflicts and then commit the result.
```

Now run:

```sh
git status
```

Read what it says carefully.

Git will have added conflict markers into the file. If you open the file in VS Code, it should help you choose how to resolve them.

After you fix the file, run:

```sh
git add stories/story.md
git commit
git push
```

If you are confused, read the message from `git status` carefully; it often tells you exactly what to do next.

## Optional: branches

If you have time, experiment with branches.

Create a branch:

```sh
git branch feature-foo
```

Switch to it:

```sh
git switch feature-foo
```

Switch back to `main`:

```sh
git switch main
```

If you look at `git log`, you should see that both branches are initially pointing to the same commit.

Now make a commit while on `feature-foo`. That commit should affect `feature-foo` but not `main`.

Use these commands to investigate:

```sh
git status
git log
git log --oneline --graph
```

If you push a branch for the first time, git may tell you to set an upstream branch. Do what it says, for example:

```sh
git push --set-upstream origin feature-foo
```

To merge `feature-foo` into `main`, do:

```sh
git switch main
git merge feature-foo
```

This will move `main` forward to include the changes from `feature-foo`.

You may need to resolve conflicts if both branches changed the same lines.

## Continue exploring

Continue experimenting with your partner.

As you do, keep checking:

```sh
git status
git log
git log --oneline --graph
```

Pay attention to how each command changes your local repository and what appears on GitHub.
