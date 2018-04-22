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
brew cask install zsh zsh completions 

curl -L https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh | sh

chsh -s /usr/local/bin/zsh

brew cask install iterm2 
```
Now close the terminal and open iTerm2, and type

```bash
echo 'export PATH="/usr/local/bin:$PATH"' >> ~/.zshrc
```
Similarly to the Homebrew instructions, this directs Zsh to use packages installed by Hombrew.
