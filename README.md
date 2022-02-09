# Local Web Development Environment Setup

The purpose of this document is to provide a step-by-step guide to set up the main software and tools I use to set up a local web development environment on a brand new installation of `macOS`.

## 1) Homebrew

Homebrew is a package manager for macOS, we'll use this to install most of the software we'll need.

- Visit the [Homebrew Website](https://brew.sh) and follow the installation instruction, it usually means just running 1 command in the Terminal.

### Updating Homebrew

```bash
brew update
```

### Upgrading all software installed using Homebrew

```bash
brew upgrade
```

## 2) iTerm2 + Oh My Zsh

iTerm2 is a replacement for `Terminal` on macOS.

- Download from the [iTerm2 Website](https://iterm2.com) and install.

Oh My Zsh provides a framework for managing zsh configuration, improving the Terminal experience.

- Visit [Oh My Zsh GitHub Repo](https://github.com/ohmyzsh/ohmyzsh) and follow the installation instruction, it usually means just running 1 command in the Terminal.

## 3) Git

Git is a version control system for tracking changes in any set of files.

- Run the following command in the Terminal:
```bash
brew install git
```
- You may want to set up some global configs for Git:
```bash
git config --global user.name "Your Name"
git config --global user.email "youremail@example.com"
```
- It is also very useful to exclude some OS and Editor specific files from Git by default. For this, you need to set up a global "gitignore" file:
```bash
touch ~/.gitignore_global
git config --global core.excludesfile ~/.gitignore_global
```
- Open the `~/.gitignore_global` file in your favorite text editor and add the content from [macOS.gitignore](https://github.com/github/gitignore/blob/main/Global/macOS.gitignore) and from [JetBrains.gitignore](https://github.com/github/gitignore/blob/main/Global/JetBrains.gitignore). You can find more gitignore examples in [GitHub's Global gitignore Repo](https://github.com/github/gitignore/tree/main/Global).

### GitHub Desktop

GitHub Desktop is an application that enables you to interact with GitHub using a GUI instead of the command line.

- Download from the [GitHub Desktop Website](https://desktop.github.com) and install.
- Authenticate the application with your account on GitHub to connect to your remote repositories.

## 4) NVM (Node Version Manager)

NVM allows you to quickly install and use different versions of `node.js` (which includes the package manager `npm`) via the command line. 

- Run the following commands in the Terminal:
```bash
brew install nvm
```
```bash
mkdir ~/.nvm
```
- Add the following lines to the `~/.zshrc` file:
```bash
export NVM_DIR="$HOME/.nvm"
[ -s "/usr/local/opt/nvm/nvm.sh" ] && . "/usr/local/opt/nvm/nvm.sh"  # This loads nvm
[ -s "/usr/local/opt/nvm/etc/bash_completion.d/nvm" ] && . "/usr/local/opt/nvm/etc/bash_completion.d/nvm"  # This loads nvm bash_completion
```
- Test the installation (you may need to restart the Terminal):
```bash
nvm --version 
```
### Managing node.js versions

- Installing the newest version:
```bash
nvm install node
```
- Installing the latest LTS release:
```bash
nvm install --lts
```
- Checking installed versions
```bash
nvm ls
```
- Changing the node.js version
```bash
nvm use xx.xx.xx
```
- Uninstalling a node.js version
```bash
nvm uninstall xx.xx.xx
```

## 5) Yarn

Yarn is a package manager for your code. 

- Run the following commands in the Terminal:
```bash
brew install yarn
```

## 6) Databases (MySQL, PostgreSQL and Redis)

MySQL, PostgreSQL are relational database management systems. A relational database organizes data into one or more data tables in which data types may be related to each other to help structure the data.

Redis is an open source, in-memory data structure store, used as a database, cache, and message broker.

### DBngin

DBngin provides a free, all-in-one database management tool that includes `MySQL`, `PostgreSQL`, and `Redis`. After DBngin has been installed, you can connect to your database at `127.0.0.1` using the `root` username and an empty string for the password.

- Download from the [DBngin Website](https://dbngin.com) and install.

### TablePlus

TablePlus is a modern, native, and friendly GUI tool for relational databases. It allows you to easily query, edit and manage your databases.

- Download from the [TablePlus Website](https://www.tableplus.io/download) and install.
- Add your license key.

## 7) PHP + Composer + Laravel

### PHP

PHP is a general-purpose scripting language geared towards web development.

- Run the following commands in the Terminal:
```bash
brew install php
```
- Test the installation (you may need to restart the Terminal):
```bash
php -v 
```

### Composer

Composer is a dependency and package manager for PHP.

- Visit the [Composer Website](https://getcomposer.org/download/) and follow the instructions (make sure to do a "global install" so you can run composer from any directory).
- Place Composer's system-wide vendor bin directory in your `$PATH` by adding the following line in the `~/.zshrc` file:
```bash
export PATH="$HOME/.composer/vendor/bin:$PATH"
```
- Test the installation by running the following commands in the Terminal:
```bash
composer
```

### Laravel Valet

Laravel Valet configures your Mac to always run `Nginx` in the background when your machine starts. It uses `DnsMasq` to proxy all requests on the `*.test` domain to point to sites installed on your local machine.

- Follow the instruction in the [Laravel Documentation](https://laravel.com/docs/master/valet#installation) (requires Composer).
- Register a directory in your machine, for example:
```bash
cd ~/Sites
valet park
```
- Now all directories within `~/Sites` will be accessible in your web browser at `http://<directory-name>.test`

### Laravel

Laravel is a web application framework that provides a structure and starting point for creating your applications.

- Install the `Laravel Installer` by following the instruction in the [Laravel Documentation](https://laravel.com/docs/master/installation#the-laravel-installer) (requires Composer).
- You can now create a Laravel app by using the following command:
```bash
laravel new example-app
``` 

## 8) Ruby + Ruby on Rails

### rbenv

rbenv is a simple Ruby version management tool which allows you to install and switch Ruby versions in your development environment.

- Run the following commands in the Terminal:
```bash
brew install rbenv
```
- Add the following lines to the `~/.zshrc` file:
```bash
export PATH="$HOME/.rbenv/bin:$PATH"
eval "$(rbenv init -)"
```
- Close and reopen the Terminal and test the installation:
```bash
rbenv install --list
```
- Install your desired `Ruby` version, for example:
```bash
rbenv install 3.1.0
rbenv rehash
```
- Test the installation (you may need to restart the Terminal):
```bash
ruby --version 
```
- List installed Ruby versions:
```bash
rbenv versions
```
- Set or show the global Ruby version:
```bash
rbenv global 3.1.0
```

### Ruby on Rails

Rails is a full-stack framework which ships with all the tools needed to build your web apps on both the front and back end.

- Run the following commands in the Terminal:
```bash
gem install rails
rbenv rehash
```
- Test the installation (you may need to restart the Terminal):
```bash
rails --version 
```
- You can now create a Rails app by using the following command:
```bash
rails new example-app
```

### Troubleshooting RubyGems for MySQL error

- In case of getting an error while installing the RubyGems for MySQL, try installing it separately with the following command:
```bash
gem install mysql2 -- --with-opt-dir="$(brew --prefix openssl)"
```
