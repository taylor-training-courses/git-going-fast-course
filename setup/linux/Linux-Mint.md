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

Append the contents of [./bash-snip.sh] into your .bashrc file.

## Configration

Minimal settings:

```bash
git config --global user.name "Your Name"
git config --global user.email "your.name@domain.com"
git config --global --list
```

Append the contents of the Git configuration file you want to use:

* Git Config with Nano editor
* Git Config with Visual Studio Code editor