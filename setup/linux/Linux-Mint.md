# Git Installation and Setup on Linux Mint

## Git Install

```bash
sudo apt install -y git
# - or -
# sudo apt-get install git
```

## Git Prompt

Download the contents of the Git Prompt script from the official Git repository:

```bash
cd ~
curl -o .git-prompt.sh https://raw.githubusercontent.com/git/git/master/contrib/completion/git-prompt.sh
```

Append the contents of [./bash-snip.sh] into your __.bashrc__ file:

```bash
if [ -f ~/.git-prompt.sh ]; then
    source ~/.git-prompt.sh
    export PS1=' \[\e[36;40m\]\u\[\e[m\]\[\e[35m\]:\[\e[m\]\[\e[33m\]\W\[\e[m\]\[\e[32m\]$(__git_ps1 "(%s)")\[\e[m\] \[\e[37m\]\\$\[\e[m\] '
else
    export PS1=" \[\e[36;40m\]\u\[\e[m\]\[\e[35m\]:\[\e[m\]\[\e[33m\]\W\[\e[m\] \[\e[37m\]\\$\[\e[m\] "
fi
```

Make sure no lines wrap.

## Configration

### Minimal Settings

Set the Git user's name and email - this will be included with every commit (change) made by you.

__User Name and Email__:

```bash
git config --global user.name "Your Name"
git config --global user.email "your.name@domain.com"
```

### Default Text Editor with Git

Set the core editor (used to edit commit messages, edit git config, etc). Your editor must already exist and the editor command needs to be accessible on the system path. Choose one of the following:

__Nano__:

Simple terminal-based editor that comes Ubuntu/Linux Mint. Great option if prefer to say within the Terminal environment.

```bash
# Nano as default editor with Git
git config --global core.editor nano
```

__Atom__:

Personal favorite, but now deprecated as it is being abandoned by Microsoft in favor of VSCode.

```bash
# Atom as default editor with Git
git config --global core.editor "atom --wait"
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
# VSCode as default editor with Git
git config --global push.default simple
```

### Default Branch Name

Git still uses "master" as the default branch name if one isn't provided, but (nearly) all Git hosting providers have adopted "main" as the default - including GitHub. I recommend changing the default locally to "main" as the default is likely to change anyway.

__Main Deafult Branch__:

```bash
# Set default branch
git config --global init.defaultBranch main
```