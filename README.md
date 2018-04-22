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
 - Typing `$ cat ~/.zshrc` into the terminal should show you the contents of the zshrc file. The bottom line should be export `PATH=“/usr/local/bin:$PATH`.
 
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
```
# Folder view configuration files
.DS_Store
Desktop.ini

# Thumbnail cache files
._*
Thumbs.db

# Files that might appear on external disks
.Spotlight-V100
.Trashes

# Compiled Python files
*.pyc

# Compiled C++ files
*.out

# Application specific files
venv
node_modules
.sass-cache
```
## Sublime Text Editor

This just installs a lightweight text editor.

*Installation & Config*

Download Sublime from http://www.sublimetext.com/. Follow the instructions to install.

To create a shortcut to use sublime, type the following into the terminal:

```bash
$ ln -s /Applications/Sublime\ Text.app/Contents/SharedSupport/bin subl /usr/local/bin/subl
```

Now you can open a document in Sublime with `$ subl filename.ext`.

## Ruby

Ruby is what the bulk of Zappi is written in. RVM is a tool that manages the Ruby version within a project.

*Installation*

```bash
$ \curl -sSL https://get.rvm.io | bash

$ source /Users/<username>/.rvm/scripts/rvm

$ rvm install ruby-2.3.3
```
Typing the above into the terminal will install RVM and Ruby version 2.3.3 (the version needed by Zappi repos).

### *IMPORTANT!!*

By default Mac OSx will use the system ruby. This should not be used during development, and it causes issues with root privileges. RVM is used to manage non-system Ruby versions. To double check that you are in fact using RVM and not system ruby, do the following:

1. Type `$ which -a ruby` into the command line. This should show

	```bash
	/Users/<user>/.rvm/rubies/ruby-2.3.3/bin/ruby
	/usr/bin/ruby
 	```

The `/usr/bin/ruby` version is the system version, with the other being the RVM version.

2. Type `$ which ruby` into the command line. You should get

	```bash
 	/Users/<user>/.rvm/rubies/ruby-2.3.3/bin/ruby
 	```

Which confirms that you are in fact using the RVM ruby.	

## Bundler

Bundler is a Ruby gem that automatically downloads gems and handles dependencies for projects. 

*Installation*

```bash
$ gem install bundler
```
**Note:** if you do not have permissions to install gems (i.e. you have to use sudo to use the “gem” command, it means you are still using the system Ruby and need to change.

## Python & Anaconda

Python is a scripting language, and houses the computational engines upon which Quattro is built. Anaconda is a distribution which bundles a whole bunch of important packages together, including NumPy, SciPy and Pandas.

*Installation*

Download Anaconda version 5.0.1 from https://repo.continuum.io/archive/Anaconda2-5.0.1-MacOSX-x86_64.pkg and install.

In the terminal, type
```bash
$ echo ‘export PATH=“$HOME/anaconda2/bin:$PATH”’ >> ~/.zshrc
```
This tells Zsh where to search for the distribution. 

To test that this has worked, type `$ which anaconda` into the terminal. It should say `Users/<username>/anaconda2/bin/anaconda`. For a further test, type `$ python` into the terminal and hit enter. You should enter the Python shell. Type `>> import numpy` and enter. If no errors are thrown it should all be good. 

## Java

Download the Mac version from http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
and install.

Test with `$ java -version`. It should show the version that you installed.

## Database Services

There are 5 database services needed to run the various Zappi repos: Postgresql, MySQL, MongoDB, Redis, and ElasticSearch. You can look up what these all do online.

It is **very important** that MySQL **version 5.6** is installed.

*Installation*

To install, use the following commands:
```bash
$ brew install mysql@5.6

$ echo 'export PATH="/usr/local/opt/mysql@5.6/bin:$PATH"' >> ~/.zshrc

$ brew install redis

$ brew install elasticsearch@2.4

$ brew install mongodb

$ brew install postgres
```
To run the Zappi repos locally, these services need to be running on your machine. To start them, type the following into the terminal:

```bash
$ brew services start mysql@5.6

$ brew services start redis

$ brew services start elasticsearch@2.4

$ brew services start mongodb

$ brew services start Postgres
```

To check that all the services are working, type `$ brew services list`. All the services should be listed along with `started`.

To provide an easy way to start these services, I recommend making a file in location `~/.start_my_services.sh` containing the following:

```bash
brew services start mysql@5.6
brew services start redis
brew services start elasticsearch@2.4
brew services start mongodb
brew services start Postgres
```
This can then be run from the terminal with `$ bash ~/.start_my_services.sh`.

# Gnu Scientific Library (GSL)

This is a library which helps with some advanced calculations. Zappi requires version 1.16.0.4 - unfortunately, this is not available with Homebrew or as a Gem, so the library has to be built from scratch with the following steps:

1. Download gsl-1.16.tar.gz from http://ftp.gnu.org/gnu/gsl/
2. Extract somewhere.
3. `$ cd` into the folder.
4. `$ /.configure`
5. `$ make`
6. `$ make install`

# Miscellaneous

The following are all necessary for various parts of the Zappi repos

Install wkhtmltopdf from https://wkhtmltopdf.org/downloads.html

```bash
$ brew install imagemagick@6
$ echo 'export PATH="/usr/local/opt/imagemagick@6/bin:$PATH"' >> ~/.zshrc
```
```bash
$ brew install icu4c
$ echo 'export PATH="/usr/local/opt/icu4c/bin:$PATH"' >> ~/.zshrc
$ echo 'export PATH="/usr/local/opt/icu4c/bins:$PATH"' >> ~/.zshrc
```
```bash
$ brew install czmq
$ brew install wget
$ brew install mc
$ brew install p7zip
$ brew install qt@5.5
$ brew install yarn
$ brew install phantomjs
$ brew install r
```
