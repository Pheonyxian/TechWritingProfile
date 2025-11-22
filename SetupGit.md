# Set Up Git from the Command Line
**Author:** Darby Vernon  
**Last Updated:** November 16, 2025  

---

## Introduction
Git is a tool that helps you keep track of changes you make to your work. It lets you go back if something breaks and makes it easy for multiple people to work on the same project without getting in each other’s way. It keeps projects organized and prevents mistakes from becoming permanent.

This guide is intended for new developers setting up Git for the first time.  
By the end, you’ll have the GitHub codebase cloned onto your local machine and be able to push changes to the repository.  
No prior knowledge of Git or the command line is required.  
**Estimated setup time:** 1 hour.

## 1. Using the Command Line

> *Skip this section if you’re already comfortable with the command line.*

The **command line** refers to a text-based interface such as **Command Prompt (Windows)** or **Terminal (macOS / Linux)**.  
Commands differ slightly between operating systems. These are the ones you’ll use most when working with Git.

### Basic Directory Navigation

| Command | Description |
|----------|-------------|
| `cd [directory]` | Change directory |
| `cd ..` | Move up one directory |
| `dir` (Windows) / `ls` (Mac/Linux) | Display files in the current directory |


### Git Commands

| Command | Description |
|----------|-------------|
| `git add [filename]` | Stage a file for commit |
| `git commit -m "message"` | Commit staged files |
| `git push` | Push commits to GitHub |
| `git push --set-upstream origin [branch]` | Required for your first push to a new branch |
| `git status` | Show changed files and current branch |
| `git fetch` | Update your list of branches |
| `git checkout [branch]` | Switch branches |
| `git checkout [filename]` | Discard changes to a file |
| `git checkout -b [branch]` | Create and switch to a new branch |
| `git pull` | Pull changes from remote |
| `git merge [branch]` | Merge another branch into your current one |
| `git mergetool` | Open a merge-conflict tool |



## 2. Installing Git
Follow GitHub’s official installation guide:  
[Install Git](https://github.com/git-guides/install-git)


## 3. Setting Up Git

1. **Create a project directory** anywhere on your computer. This is where your code will live.
2. **Clone the repository:**
   - On the project’s GitHub page, click the green **Code** button.  
   - Select the **SSH** tab and copy the URL (starts with `git@`).  
   - While HTTP cloning works, SSH is more secure and avoids authentication issues.
3. **Open your terminal** and navigate to the directory you just created:
   ```
   cd path/to/your/folder
   git clone [git url you just copied]
   ```

## 4. Setting Up SSH
SSH (“Secure Shell”) provides encrypted communication with GitHub, ensuring only authorized users can push code.

1. **Generate an SSH key:**
[GitHub guide: Generating a new SSH key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent?platform=windows)

2. **Add your key to GitHub:**
[GitHub guide: Add SSH key to your account](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)

3. **Set your global configuration:**
	```
	git config --global user.email "you@example.com"
	git config --global user.name "Your Name"
	git config --global url."git@github.com:".insteadOf "https://github.com/"
	```

4. **Verify configuration:**
	```
	git config --global --list
	```
	The Command Line should return the information you just set.

5. **Test your connection:**
[Test your SSH connection](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/testing-your-ssh-connection)

## 5. Typical Workflow
A standard feature workflow looks like this:

1. **Ensure you're on the main branch:**
	```
	git checkout main
	git pull
	```

2. **Create a feature branch:**
	```
	git checkout -b feature/your-branch-name
	```
3. **Edit your code** in your preferred editor.
4. **Stage your changes:**
	```
	git add [filename]
	```
	If you have multiple files that have changed and you would like to stage them all, you can use the command
	```
	git add .
	```

5. **(Optional) Check the status of your staged files:**
If you want to double check which files are currently staged, use the command
	```
	git status
	```
	It's a good idea to check your staged files when using `git add .` to ensure you're not adding unexpected files.

6. **Commit your work:**
	```
	git commit -m"Describe your change"
	```
7. **Push to the remote branch:**
	If this is the first time you're pushing to your new branch, you'll need to use:
	```
	git push --set-upstream origin feature/your-branch-name
	```
	Everytime thereafter, you can shorten this to :
	```
	git push
	```
8. **Confirm your branch** appears on GitHub in the Branches tab.

## Troubleshooting
Below are common problems developers encounter when using Git.
| Problem | Likely Cause | Solution |
|----------|-------------|----------|
|`Permission denied (publickey)`|SSH key not added or GitHub not configured|Revisit SSH setup guide|
|`fatal: not a git repository`|Command run outside a cloned repo|Use `cd` to navigate to the project folder|
|`could not resolve host github.com`|No internet connection or network proxy|Check your network or run `git config --global --unset http.proxy`|
|Authentication prompts every push|Using HTTPS instead of SSH|Update remote URL: `git remote set-url origin git@github.com:user/repo.git`|
|Merge conflicts when pulling|Overlapping changes between branches|Run `git mergetool` to resolve, then `git commit`|
|Branch not showing on GitHub|Push missing `--set-upstream`|Push again: `git push --set-upstream origin [branch]`|

**Pro Tip:** If your terminal ever looks "stuck," press **Ctrl + C** to safely cancel the current operation.

## 7. Next Steps
* Learn about your team's branching strategies and naming conventions. Most teams will have a main branch, develop branch, several feature branches, and prefer if you name your personal working branches something like "[name]-[JIRA ticket]"
* Explore the mergetool. Settling merge conflicts is very common. Feel free to find a tool other than the default if you'd prefer.
* Explore `git log` and `git diff` to view commit history.
* Learn `git stash` and `git revert` for version control safety.
