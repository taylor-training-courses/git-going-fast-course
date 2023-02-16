# Git Installation and Setup on Linux Mint

Instructions are provided for those that prefer to do this themselves.

> Note: A user with __sudo__ is required for these instructions.

### Tested Versions

* Linux Mint 21.1

Should work with all recent versions of Linux Mint.

### Update Apt

Let's make sure all existing packages are already updated.

```bash
sudo apt update
sudo apt upgrade
```

## Git Install

Pick one of the following:

__Apt / Aptitude__:

This is better for interactive terminal sessions.

```bash
sudo apt install git
```

or

__Apt-Get__:

This is better for automation scripts.

```bash
sudo apt-get install -y git
```

Note: The __-y__ option is to auto accept at the prompt.

## Git Prompt

Download the contents of the Git Prompt script from the official Git repository:

```bash
cd ~
curl -o .git-prompt.sh https://raw.githubusercontent.com/git/git/master/contrib/completion/git-prompt.sh
```

Append the contents of this into your __.bashrc__ file (Linux Mint uses Bash as the default user shell):

```bash
if [ -f ~/.git-prompt.sh ]; then
    source ~/.git-prompt.sh
    export PS1=' \[\e[36;40m\]\u\[\e[m\]\[\e[35m\]:\[\e[m\]\[\e[33m\]\W\[\e[m\]\[\e[32m\]$(__git_ps1 "(%s)")\[\e[m\] \[\e[37m\]\\$\[\e[m\] '
else
    export PS1=" \[\e[36;40m\]\u\[\e[m\]\[\e[35m\]:\[\e[m\]\[\e[33m\]\W\[\e[m\] \[\e[37m\]\\$\[\e[m\] "
fi
```

Make sure no lines wrap. If you use a different shell, make adjustments accordingly.

## Configuration

Git requires a bit of configuration before allowing us to do very much with it.

### Minimal Settings

Set the Git user's name and email - this will be included with every commit (change) made by you.

__User Name and Email__:

```bash
git config --global user.name "Your Name"
git config --global user.email "your.name@domain.com"
```

### Default Text Editor with Git

Set the core editor (used to edit commit messages, edit git config, etc). Your editor must already exist and the editor command needs to be accessible on the system path. Choose one of the following. This course uses Visual Studio Code.

__Nano__:

Simple terminal-based editor that comes Ubuntu/Linux Mint. Great option if prefer to say within the Terminal environment.

```bash
# Nano as default editor with Git
git config --global core.editor nano
```

__Visual Studio Code__:

Used with Git Going Fast course.

```bash
# VSCode as default editor with Git
git config --global core.editor "code --wait"
```

### Default Push Behavior

The old default was to push all changes on all branches. The new default (2.x) is to only push changes on the same branch, however, not setting this explicity caused Git to warn you about the change.

__Simple Pushing__:

```bash
# Use "simple" behavior for pushing
git config --global push.default simple
```

### Default Branch Name

Git still uses "master" as the default branch name if one isn't provided, but (nearly) all Git hosting providers have adopted "main" as the default - including GitHub. I recommend changing the default locally to "main" as the default is likely to change soon anyway.

__Main Default Branch__:

```bash
# Set default branch
git config --global init.defaultBranch main
```

## Visual Studio Code

This course uses [Visual Studio Code][vscode] as the primary code editor since it is cross-platform and available on all operating systems supported by this course.

Go to the [Visual Studio Code][vscode] website. The web page should detect you are browsing on a Linux platform and offer you the choice between an RPM (RedHat family) or DEB package (Debian family). Since Linux Mint is part of the Debian family, choose to download the Deb package.

Once the Visual Studio Code DEB package is downloaded, open or Show in Folder. With the folder open, right-click on the package and choose to install with the Package installer - which should be the defualt action. When that opens, click the green "Install Package" button.

Package Installer will ask you to authenticate - just provide your user's password - this will require __sudo__ access.

Once the package is installed, close the Package Installer. At this point Visual Studio Code should be installed.

At this point, I recommend adding it as a favorite, to the panel and possibly to the Desktop for easy access. I also recommend opening up your terminal application and confirming the `code` command is available.

```bash
which code
code --version
code .
```

Upon opening VSCode, you may want to adjust the size of the interface for better readability - I'm doing to do this so code shows up better throughout the course.

## Conclusion

These are all the tools needed for the Git Going Fast course.



[vscode]: https://code.visualstudio.com/ "A code editor from Microsoft that doesn't suck"