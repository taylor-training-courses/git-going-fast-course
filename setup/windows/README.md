# Git Installation and Setup on Windows 10/11

Instructions are provided for those that prefer to do this themselves. This guide should work for both Windows 10 (add editions) and Windows 11 (all edition) - differences between the two will be mentioned where required.

> Note: A user with administrative rights is recommended to install software - if installing for all users on the system. For single user account, local install should be supported.

### Tested Versions

* Windows 10
    * Windows 10 Home
    * Windows 10 Pro
* Windows 11
    * Windows 11 Home
    * Windows 11 Pro

Should work without issue on Education and Enterprise editions, including "N" or other variants.

### Update System and Store Apps

Run Windows Update to make sure you have the latest updates possible before starting. Additionally, so the same within the Microsoft Store (especially on Windows 11).

### Requirements

* Modern web browser or Google Chrome
* Windows Terminal (from Microsoft Store) - optional, but highly recommended.

> Note: Windows 10 requires Windows Terminal be installed (free) via the Microsoft Store.

> Note: While Windows 11 comes with Windows Terminal. It still needs to be updated via the Microsoft Store before installing Git.

## Visual Studio Code (aka VSCode)

> You can install VSCode either before _or_ after installing Git.

This course uses [Visual Studio Code][vscode] as the primary code editor since it is cross-platform and available on all operating systems supported by this course. Go to the [Visual Studio Code][vscode] website. The web page should detect you are browsing on a Windows system and offer you the correct installer.

### Installation

Once the installer is downloaded, run the installer. 

Setup > Additional Tasks:

* Check all items

Assume defaults unless specified above.

### Icons

I like to add or ensure the VSCode icon is available:

* Desktop
* Start Menu
* Taskbar

### Code Command

After the installation, open your Terminal/Command Prompt and type:

```bash
code
```

This should open VSCode directly from you Terminal application.

### Resize to Taste

You can use the keyboard shortcut "Ctrl and Plus" together to increase the user interface, including text contents. For my screen, I did this 4 times to reach a nice readability on my screen.

### Done

VSCode should be installed. The integration with Git will be covered in the Git section.

## Git Install

With all the requirements in place, let's install Git from the official [Git Website][git] - which should detect you are running on Windows and offer the correct installer directly from the homepage. If, for some reason, the download does not automatically start, you can click the link manually on the download page.

### Installation

Once the installer is downloaded, run the installer. 

Setup > Select Components:

* Check all items

> Give me all the options!

Setup > Choosing the default editor used by Git:

* Select "nano" (first item - many need to scroll up to see it)

> You _can_ simply select your preferred editor if it is listed.

Setup > Configuring the line ending conversions:

* Checkout as is, commit Unix-style endings (middle option)

> Best for cross-platform teams

Assume defaults unless specified above. New pages are often added as the Git installer is updated - occasionally, exisitng pages are revised or removed. I recommend leaving anything on the "Experimental" page _unchecked_.

### Git Bash

You can adjust the size, rows and columns used by Git Bash by editing the Options page by right-clicking on the Git Bash window title bar once opened. I normally have to save and try my settings out several times before landing on my preferred settings. Remember to __Save__ the changes.

Once Git Bash is setup as desired, add Git Bash to:

* Desktop (default)
* Taskbar
* Start Menu

### Windows Terminal - Git Bash Profile

If, during the installation process, you checked the option to integrate Git Bash with a Windows Terminal profile (Select Components page), then you should have a Git Bash profile in your Terminal app. Normally, this still requires a bit of tweaking to adjust the font size, rows and columns - just like with Git Bash.

> Note: Windows 10 requires Windows Terminal be installed (free) via the Microsoft Store first.

> Note: While Windows 11 comes with Windows Terminal. It still needs to be updated via the Microsoft Store before installing Git.


### Git Prompt

While the default prompt integrated with Git Bash is acceptable, it is not as compact (single line) as it should be. To address that, I like to use a special script called "Git Prompt."

Make sure you are in your user's home directory (default):

```bash
cd ~
```

First, we need to ensure Git Bash is ready. We need to create two startup scripts:

```bash
code .bashrc
```

Contents of __.bashrc__:

```bash
if [ -f ~/.bashrc ]; then
    source ~/.bashrc
fi
```

It is possible this file already exists. Just confirm the contents looks like above. Save and close the file.

```bash
code .bash_profile
```

Contents of __.bash_profile__:

```bash
export LS_COLORS="di=36;40:ln=32;40:so=32:pi=33:ex=31;40:bd=34;46:cd=34;43:su=30;41:sg=30;46:tw=1;32;40:ow=32;40"
export EDITOR=nano

alias ll="ls -AlGh -I 'ntuser*' -I 'NTUSER*'"

if [ -f ~/.git-prompt.sh ]; then
    source ~/.git-prompt.sh
    export PS1=' \[\e[36;40m\]\u\[\e[m\]\[\e[35m\]:\[\e[m\]\[\e[33m\]\W\[\e[m\]\[\e[32m\]$(__git_ps1 "(%s)")\[\e[m\] \[\e[37m\]\\$\[\e[m\] '
else
    export PS1=" \[\e[36;40m\]\u\[\e[m\]\[\e[35m\]:\[\e[m\]\[\e[33m\]\W\[\e[m\] \[\e[37m\]\\$\[\e[m\] "
fi
```

> When you save this file, make sure no lines are wrapping - this might messup script execution.

The _ll_ alias is specific for Windows and it replicates how is should work on a Linux system. This is included becuase I like using this command and it has become a habit.

Save and close the file.

Download the contents of the Git Prompt script from the official Git repository:

```bash
curl -o .git-prompt.sh https://raw.githubusercontent.com/git/git/master/contrib/completion/git-prompt.sh
```

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


## Conclusion

These are all the tools needed for the Git Going Fast course. If you followed this instruction guide, you can continue along starting with the next chapter.



[vscode]: https://code.visualstudio.com/ "A code editor from Microsoft that doesn't suck"
[git]: https://git-scm.com/ "Git SCM website"