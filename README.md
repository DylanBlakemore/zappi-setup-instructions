# Zappi Setup Instructions

## Homebrew

This is a package manager for Mac OS X.

*Installation*

Type the following commands into the terminal:

```bash
$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)” 

$ echo 'export PATH="/usr/local/bin:$PATH"' >> ~/.bash_profile 
```

This downloads and instals Homebrew, as well as directing the system to use software installed by Homebrew rather than possible default versions. Close the terminal and reopen a new window.

## Zsh and iTerm2

Combined, Zsh ("Zed shell") and iTerm2 provide customisation tools for the terminal, including themes, keyword completion, and extended window splitting capabilities.

*Installation*

Type the following into the terminal: 

```bash
$ brew cask install zsh zsh-completions 

$ curl -L https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh | sh

$ chsh -s /usr/local/bin/zsh

$ brew cask install iterm2 
```
This installs (in order) Zsh, Zsh-completions and Oh My Zsh. It then sets Zsh as the default terminal. Finally, it installs iTerm2.

Now close the terminal and open iTerm2, and type

```bash
$ echo 'export PATH="/usr/local/bin:$PATH"' >> ~/.zshrc
```
Similarly to the Homebrew instructions, this directs Zsh to use packages installed by Hombrew.

### Sanity Checks
 - Terminal should have “(zsh)” somewhere at the top.
 - Typing `cat ~/.zshrc` into the terminal should show you the contents of the zshrc file. The bottom line should be export `PATH=“/usr/local/bin:$PATH`.
 
 ## Git and SSH Keys
 
 Git is the most popular version control system. You will need a Github account to complete these steps, so do that first.
 
 *Git Installation & Config*
 
 Type the following into your terminal:
 ```bash
$ brew install git

$ git config --global user.name “Your Name”

$ git config --global user.email “your_email@example.com"  

$ git config --global credential.helper osxkeychain
```
This installs git and sets up the global variables (Note that "Your Name" and the email address should be replaced by the values you used in setting up your Github account).
The last command enables password caching to save you some time when pulling/pushing/cloning/whatever.

Now type the following into the terminal:

```bash
$ ssh-keygen -t rsa -C "your_email@example.com"

$ eval “$(ssh-agent -s)”

$ ssh-add -K ~/.ssh/id_rsa

$ git config —global core.excludesfile ~/.gitignore
```

In order, this will
1. Generate a public and private SSH key
2. Add the key to a local SSH agent
3. Create a global .gitignore file which will be used by all git projects.

Now add the public key to your SSH keys on Github (Settings->SSH and GPG Keys->New SSH Key). The contents of the key are found in `~/.ssh/id_rsa.pub`.

Finally, open up the file `~/.gitignore` and paste into it the contents below:

> \# Folder view configuration files

> .DS_Store

> Desktop.ini
>
> \# Thumbnail cache files
> ._*
> Thumbs.db
>
> \# Files that might appear on external disks
> .Spotlight-V100
> .Trashes
>
> \# Compiled Python files
> *.pyc
>
> \# Compiled C++ files
> *.out
>
> \# Application specific files
> venv
> node_modules
> .sass-cache
