# Rails Setup Guide For Ubuntu

The purpose of this step by step tutorial is to provide a very simple example of configuring a minimal Rails environment.

## Software Requirements

- Ubuntu 18.04 or later

- 16 GB RAM minimum

## Pre-Installation Steps

[Download Ubuntu Desktop](https://www.ubuntu.com/download/desktop/thank-you?version=18.04.2&architecture=amd64)

## Installation Steps

1.  In Ubuntu, download and install general development tools

    ```bash
    sudo apt-get update -y && sudo apt-get install -qq -y --no-install-recommends \
    autoconf \
    bash \
    bash-completion \
    bison \
    build-essential \
    ctags \
    curl \
    git-core \
    imagemagick \
    libcurl3-dev \
    libffi-dev \
    libgdbm-dev \
    libgdbm5 \
    libmagick++-6-headers \
    libncurses5-dev \
    libreadline6-dev \
    libssl-dev \
    libyaml-dev \
    locales \
    lsb-release \
    nodejs \
    openssh-server \
    software-properties-common \
    sudo \
    unzip \
    yarn \
    zlib1g-dev
    ```

2.  In Ubuntu, download and install PostreSQL

    ```bash
    sudo apt-get update && sudo apt-get install -y gnupg2 wget
    wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
    sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ $(lsb_release -sc)-pgdg main" > /etc/apt/sources.list.d/PostgreSQL.list'
    sudo apt-get update -y -qq && sudo apt-get upgrade -y -qq
    sudo apt-get install -y -qq \
      libpq-dev \
      postgresql-11 \
      postgresql-client-11 \
      postgresql-server-dev-11
    ```

3.  In Ubuntu, start the PostgreSQL

    ```bash
    sudo service postgresql start
    ```

4.  In Ubuntu, set the default PostgreSQL password

    - login into the `postgres` account

      ```bash
      sudo su - postgres
      ```

    - start the `psql` client application

      ```bash
      psql
      ```

      If everything went successful, one should see something similar to the following:

      ```text
      postgres@6d0d30345e56:~$ psql
      psql (10.5 (Ubuntu 10.5-1.pgdg16.04+1))
      Type "help" for help.

      postgres=#
      ```

    - change the PostgreSQL password by typing the following into the prompt and hitting the enter key:

      ```text
      \password
      ```

    - enter `password` for `Enter new password:` prompt.

    - enter `password` for `Enter it again:` prompt.

    - exit `psql` prompt by typing the following into the prompt and hitting the
      enter key:

      ```text
      \q
      ```

    - exit `postgres` account by typing the following:

      ```bash
      exit
      ```

    Note: The password that you'll be using within your `database.yml` file
    will be `password`.

5.  In Ubuntu, download and install Node

    ```bash
    curl -sL https://deb.nodesource.com/setup_11.x | sudo -E bash -
    sudo apt-get update -y && sudo apt-get install -y nodejs
    ```

6.  Install Visual Studio Code Insiders

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
    sudo install -o root -g root -m 644 microsoft.gpg /etc/apt/trusted.gpg.d/
    sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main" > /etc/apt/sources.list.d/vscode.list'
    sudo apt-get install apt-transport-https
    sudo apt-get update
    sudo apt-get install code-insiders
    ```

7.  Create an alias for Visual Studio Code - Insiders

    ```bash
    echo 'alias c="code-insiders"' >> ~/.bashrc
    ```

8.  In Ubuntu, clone this repository

    ```bash
    cd $HOME
    git clone https://github.com/conradwt/rails-setup-guide-for-ubuntu
    ```

9.  In Ubuntu, change directory to the cloned repository

    ```bash
    cd rails-setup-guide-for-ubuntu
    ```

10. In Ubuntu, install and configure RBenv

    ```bash
    git clone https://github.com/sstephenson/rbenv.git ~/.rbenv
    sudo chmod go-w $HOME/.rbenv
    cd ~/.rbenv && src/configure && make -C src
    echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
    source $HOME/.bashrc
    echo 'eval "$(rbenv init -)"' >> ~/.bashrc
    source $HOME/.bashrc
    ```

11. In Ubuntu, install all of the approved plugins RBenv plugins

    ```bash
    cd $HOME/rails-setup-guide-for-ubuntu
    chmod +x install-rbenv-plugins.bash
    ./install-rbenv-plugins.bash
    ```

12. In Ubuntu, install Ruby

    ```bash
    rbenv install 2.6.2
    rbenv global 2.6.2
    ```

13. In Ubuntu, install Bundler and Rails

    ```bash
    gem install bundler -v=1.17.3
    gem install rails
    gem install rubocop
    rbenv rehash
    ```

14. In Ubuntu, set the Git completion

    ```bash
    cp $HOME/rails-setup-guide-for-ubuntu/sample.git-completion.sh $HOME/.git-completion.sh
    echo 'source $HOME/.git-completion.sh' >> $HOME/.bashrc
    ```

15. In Ubuntu, install Heroku Toolbelt

    ```bash
    curl https://cli-assets.heroku.com/install-ubuntu.sh | sh
    ```

16. In Ubuntu, create a Github.com account

    ```
    Note:  Skip this step if you already have an account.
    ```

17. In Ubuntu, create Git configuration and global files

    ```
    cp $HOME/rails-setup-guide-for-ubuntu/sample.gitconfig ~/.gitconfig
    cp $HOME/rails-setup-guide-for-ubuntu/sample.gitignore_global ~/.gitignore_global
    ```

18. In Ubuntu, edit .gitconfig file

    - change `excludesfile` setting:

      ```bash
      git config --global core.excludesfile ~/.gitignore_global
      ```

    - change `name` and `email` for Github account

      e.g.

      ```bash
      git config --global user.name "John Doe"
      git config --global user.email johndoe@example.com
      ```

19. In Ubuntu, create and/or setup SSH keys

    - have existing ssh keys

      - create SSH folder in home directory

        ```bash
        mkdir -p $HOME/.ssh
        ```

      - copy your SSH keys to the above folder

      - set permissions

        ```bash
        chmod 700 $HOME/.ssh
        chmod 600 $HOME/id_rsa
        chmod 644 $HOME/id_rsa.pub
        ```

    - doesn't have existing ssh keys

      - [Generating a new SSH key and adding it to the ssh-agent](https://help.github.com/en/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

        Note: Please select Linux link at the top of the page.

20. Add SSH public key to Github

    [Adding a new SSH key to your GitHub account](https://help.github.com/en/articles/adding-a-new-ssh-key-to-your-github-account)

## Support

Bug reports and feature requests can be filed here:

- [File Bug Reports and Features](https://github.com/conradwt/rails-setup-guide-for-ubuntu/issues)

## Contact

Follow Conrad Taylor on Twitter ([@conradwt](https://twitter.com/conradwt))

## Creator

- [Conrad Taylor](http://github.com/conradwt) ([@conradwt](https://twitter.com/conradwt))

## License

This repository is released under the [MIT License](http://www.opensource.org/licenses/MIT).

## Copyright

&copy; Copyright 2018 - 2019 Conrad Taylor. All Rights Reserved.
