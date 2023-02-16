# Git Installation and Setup on MacOS

Instructions are provided for those that prefer to do this themselves. As of 2023, these instructions will work on both Intel and Apple Silicon based Macs.

## Requirements

* Use the Terminal App (Applications > Utilities)
* [Apple Developer Command Line Tools](#apple-developer-command-line-tools--apple-git)
* [iTerm 2](#iterm-2) (https://iterm2.com/) (Optional)
* [Oh My Zsh!](#oh-my-zsh) (https://ohmyz.sh/) (Optional)
* [Homebrew](#homebrew) (https://brew.sh/) (Optional)
* Admin / sudo rights / ability to install software on your system

Use the Terminal App to install the Command Line tools, then install iTerm2, then Oh My Zsh, and finally, Homebrew. Technically, Apple Git (comes with the Command Line tools) is sufficient for this course, but I use the version installed by [Homebrew](#homebrew) because it tends to be more updated. However, if you decide to stick with Apple Git, you may want to use [Git Prompt](#git-prompt) to display the branch name while in a Git-managed directory - see the [Git Prompt](#git-prompt) section for instructions for that.

### Apple Developer Command-Line Tools / Apple Git

The command-line tools are being included with the Operating System recently, but if they are not included, they can be installed with the following command:

```bash
xcode-select --install
```

Note: Sometimes major Operating System updates will break the Command Line tools - you can run the above command to fix this.

You can test to see if Git is installed via the Command Line tools like this:

```bash
git version
```

At this point, you technically have everything needed to continue the course, but recommend installing Git via Homebrew anyway.

### iTerm 2

[iTerm 2](https://iterm2.com/ "iTerm 2 - A replacement terminal for MacOS") is a brilliant replacement to the standard Terminal app included with MacOS. If you are content with the Terminal app, this is very optional.

iTerm 2 requires the Command Line Tools to be installed first - so, ironicaly, you may need to use Apple Terminal to install iTerm2.

Installation:

* Go to https://iterm2.com/ website
* Downloads page
* Download the latest "stable" zip file
* Expand the zip file
* Move the iTerm app into the Applications folder
* Run iTerm from Applications
* Edit preferences / profile to adjust Text / Window size to taste

Upon first running of the iTerm app, MacOS will prompt to make sure you really want to run this _and_ iTerm may need to download some additional packages.

At this point, "terminal app/application" will refer to either the Apple Terminal app or iTerm 2 - which ever you have installed and prefer to use.

### Oh My Zsh

MacOS now uses Zsh as the default user shell instead of Bash. There is a nice project that greatly improves the Zsh experience called [Oh My Zsh!](https://ohmyz.sh/ "Oh My Z - improvements to Zsh for MacOS"). For the purpose of this course, what OhMyZ provides is an easy way to add Git branch information directly within the terminal prompt. If you prefer not to use this script, consider using the "Git Prompt" script instead.

Just follow the instructions from the website, or this line from within your terminal application:

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

After installation, restart your terminal session/app.

### Homebrew

MacOS does not come with a package manager like many Linux distributions do (apt/yum/dnf), however there is a command line utility that provides that ability called [Homebrew](https://brew.sh/ "Homebrew - this missing package manager for MacOS"). Many IT professionals already have Homebrew installed, so using it to install Git and other packages is a natural way to go.

Just follow the instructions from the website, or this line from within your terminal application:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

After install, restart your terminal session/application.

#### Missing Brew Command on Apple Silicon Macs

On Apple Silicon machines, your __brew__ command might not be found, even after restarting your terminal application. To fix this, add Homebrew's path to your system path:

Append to __~/.zshrc__:

```
export PATH=/opt/homebrew/bin:$PATH
```

Of course, adjust if you are using Bash or another shell. Also, keep the Homebrew path ahead of all other paths so anything installed here will take priority.


## Installing Git

Overview:

* Apple Git path and version
* Install Git via Homebrew (optional)
* Confirm Git installed via Homebrew

### Git Path and Version

To verify we have installed Git, we need to run the following commands:

__Where is Git installed right now?__:

```bash
which git
```

__Version of Git__:

```bash
git version
```

At this point, we should have Apple's version of Git installed within the default system location. This should be fine for this course, but continue on to install Git via Homebrew.

### Git Installation

Assuming you will be following along with the course, install Git via Homebrew. Homebrew typically has a more updated version of Git, which is why I prefer this method.

```bash
brew install git
```

With Git installed (again), let's confirm we are getting the Homebrew installed version:

```bash
which git
git version
```

Both commands should display something different than before. If you still see the Apple version of Git, restart your terminal session and try again.


## Git Prompt

> __NOTE__: Only follow these instructions if opting __not__ to use *Oh My Zsh* since that project accomplishes a similar result. If not installing Git Prompt, skip down to the [Git Configuration](#configuration) section.

Download the contents of the Git Prompt script from the official Git repository:

```bash
cd ~
curl -o .git-prompt.sh https://raw.githubusercontent.com/git/git/master/contrib/completion/git-prompt.sh
```

Append the contents of this into your __.zshrc__ file (MacOS uses Zsh as the user shell by default):

```bash
export CLICOLOR=1
export LSCOLORS=gacacxdxbaegedabagCaca
export EDITOR=nano

alias ll="ls -Alh"

if [ -f ~/.git-prompt.sh ]; then
    source ~/.git-prompt.sh
    export PS1=' \[\e[36;40m\]\u\[\e[m\]\[\e[35m\]:\[\e[m\]\[\e[33m\]\W\[\e[m\]\[\e[32m\]$(__git_ps1 "(%s)")\[\e[m\] \[\e[37m\]\\$\[\e[m\] '
else
    export PS1=" \[\e[36;40m\]\u\[\e[m\]\[\e[35m\]:\[\e[m\]\[\e[33m\]\W\[\e[m\] \[\e[37m\]\\$\[\e[m\] "
fi
```

The first three lines are very option and can be excluded if preferred. The __alias__ line creates the `ll` command since I'm very used to using that, but it is also optional. The last lines are what really needed to be appended to your shell's startup file.

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

Obviously, provide your actual name and email address. If concerned about privacy, GitHub does provide a private email setting that can be used (covered within the course).

### Default Text Editor with Git

Set the core editor (used to edit commit messages, edit git config, etc). Your editor must already exist and the editor command needs to be accessible on the system path. Choose one of the following. This course uses Visual Studio Code.

__Nano__:

Simple terminal-based editor that comes MacOS. Great option if prefer to say within the Terminal environment.

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

Note: Visual Studio Code must be installed first or simply add this setting after VSCode is installed.

### Default Push Behavior

The old default was to push all changes on all branches. The new default (2.x) is to only push changes on the same branch, however, not setting this explicity caused Git to warn you about the change.

__Simple Pushing__:

```bash
# Use "simple" behavior for pushing
git config --global push.default simple
```

### Default Branch Name

Git still uses "master" as the default branch name if one isn't provided, but (nearly) all Git hosting providers have adopted "main" as the default - including GitHub. I recommend changing the default locally to "main" as the default is likely to change anyway.

__Main Default Branch__:

```bash
# Set default branch
git config --global init.defaultBranch main
```

### Default Pager

For some reason, Git on MacOS may use a pager (helper program) even when a pager is not required. To fix this, set the default pager.

__Fix the Pager__:

```bash
# fix the pager
git config --global core.pager "less -X -F"
```
