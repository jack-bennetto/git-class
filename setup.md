
# Setup Lab: Git + VS Code + GitHub for Windows

## Goal

By the end of this setup, you should have:

- Git installed on your Windows computer
- Visual Studio Code (VS Code) installed
- A GitHub account
- VS Code connected to GitHub
- A simple test repository you can push to and pull from without using the terminal

---

## Part 1: Install Git

1. Open the official Git download page for Windows.
2. Download the standard Windows installer.
3. Run the installer.
4. If you are not sure what to choose during installation, just keep the default options.
5. Finish the installation.

### Notes

- Git is the tool that tracks changes to files.
- On Windows, the official Git for Windows installer is the normal place to get Git.
- If the installer asks about a credential helper, keep the recommended Git Credential Manager option if it is already selected.

### Windows — Make sure Git is on your PATH

After installation you should be able to run `git --version` in a terminal. If that command fails, Git is not on your PATH and you won't be able to run `git config --global ...` from PowerShell or Command Prompt until you add it.

PowerShell (quick, recommended):

1. Open a new **PowerShell** window as your normal user.
2. Run the following to add the typical Git install location to your user PATH (this persists for future sessions):

```powershell
$gitPath = 'C:\Program Files\Git\cmd'
if (-not ($env:Path -split ';' | Where-Object { $_ -eq $gitPath })) {
   [Environment]::SetEnvironmentVariable('Path', $env:Path + ';' + $gitPath, 'User')
}
```

3. Close and re-open PowerShell (or sign out/in) so the updated PATH is applied. To check immediately in the reopened shell run:

```powershell
git --version
```

If you only want the change for the current shell session (temporary), run:

```powershell
$env:Path += ';C:\Program Files\Git\cmd'
git --version
```

Manual (Windows Settings):

1. Open Start → type **Environment Variables** → choose **Edit the system environment variables**.
2. In the System Properties window click **Environment Variables...**.
3. Under **User variables for [user.name]** select the `Path` variable and click **Edit...**.
4. Click **New** and add the path `C:\Program Files\Git\cmd` (or the folder where you installed Git).
5. Click **OK** on all dialogs, then close and re-open your terminal and run `git --version` to verify.

Notes:

- Typical Git install locations are `C:\Program Files\Git\cmd` or `C:\Program Files\Git\bin` depending on installer options. Use the one that exists on your machine.
- After verifying `git --version` works, set your identity for commits (required for this lab):

```powershell
git config --global user.name "Your Name"
git config --global user.email "you@company.com"
```

Official references:

- [Git for Windows install page](https://git-scm.com/install/windows)
- [Pro Git: Installing Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

---

## Part 2: Install Visual Studio Code

1. Open the official VS Code download page.
2. Download the **Windows User Installer**.
3. Run the installer.
4. Accept the defaults unless your organization has told you otherwise.
5. Open VS Code after installation.

### Notes

- VS Code is a free editor that includes built-in Git support.
- You do **not** need to learn terminal commands for this lab.

Official references:

- [VS Code download page](https://code.visualstudio.com/download)
- [VS Code setup on Windows](https://code.visualstudio.com/docs/setup/windows)

---

## Part 3: Create a GitHub Account

1. Go to GitHub.
2. Click **Sign up**.
3. Follow the prompts to create an account **with your slalom address**.
4. Verify your email address if GitHub asks you to.


Official reference:

- [Creating an account on GitHub](https://docs.github.com/en/get-started/start-your-journey/creating-an-account-on-github)

---

## Part 4: Sign In to GitHub from VS Code

This is the easiest way to connect GitHub to Git on your computer.

1. Open **VS Code**.
2. Create a new folder somewhere easy to find, such as on your Desktop. This is where all your git repositories will live.
   - Example: `git`
3. Create a new folder inside of that for a test.
   - Example: `git-test`

4. In VS Code, open that folder.
5. Click the **Source Control** icon on the left side.
6. Click **Initialize Repository**.
7. Create a new file called `README.md`.
8. Add one line of text, such as:

   `My first Git practice repository`

9. Save the file.
10. In **Source Control**, type a short commit message, such as:

   `Initial commit`

11. Click **Commit**.
12. Click **Publish to GitHub**.
13. If prompted, choose **Sign in**.
14. Your browser should open. Sign in to GitHub there and approve the connection.
15. Return to VS Code.
16. Choose whether to create the repository as **Private** or **Public**.
    - For training, **Private** is usually the safer default.
17. Finish the publish step.

### What just happened?

You have now:

- created a local Git repository on your computer
- saved your first commit
- connected VS Code to GitHub
- pushed your repository to GitHub

Official references:

- [VS Code source control overview](https://code.visualstudio.com/docs/sourcecontrol/overview)
- [Using GitHub in VS Code](https://code.visualstudio.com/docs/sourcecontrol/github)

---

## Troubleshooting

### “VS Code says Git is not installed”

Git probably was not installed yet, or VS Code was open during installation.

Try this:

1. Close VS Code
2. Install Git
3. Re-open VS Code

Official references:

- [Pro Git: Installing Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- [VS Code setup on Windows](https://code.visualstudio.com/docs/setup/windows)

### “It asks for a password when pushing”

Do **not** use your GitHub account password for Git operations.

GitHub no longer allows password-based authentication for Git. Use the browser sign-in flow in VS Code, or use a credential helper or token if your instructor specifically asks you to.

Official reference:

- [About authentication to GitHub](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/about-authentication-to-github)

### “The browser opened, but VS Code did not finish signing in”

Try this:

1. Go back to VS Code manually
2. Close VS Code and reopen it
3. Repeat the **Publish to GitHub** step

### “I’m already signed into GitHub in the browser”

That is fine. VS Code may use that existing browser session to finish authentication.

Official reference:

- [Using GitHub in VS Code](https://code.visualstudio.com/docs/sourcecontrol/github)

### “Public or Private?”

If you are unsure, choose **Private**.

---

## Official Help Links

- [Git for Windows install docs](https://git-scm.com/install/windows)
- [VS Code Windows install docs](https://code.visualstudio.com/docs/setup/windows)
- [GitHub account creation docs](https://docs.github.com/en/get-started/start-your-journey/creating-an-account-on-github)
- [VS Code + GitHub docs](https://code.visualstudio.com/docs/sourcecontrol/github)

