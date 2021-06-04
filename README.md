# ruby-on-rails
Instructions for Ruby on Rails installations in Windows 10
Versions:
Ruby: ruby 2.5.0p0 (2017-12-25 revision 61468) [x86_64-linux]
Rails: Rails 6.0.2
Ruby Installations:
We need to install Window Subsystem for Linux because Windows allows to use linux VM, 
So install ubuntu and run the commands in ubuntu command line.

First of all we need to 
Open Powershell as Administrator and run:
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
Next install Ubuntu from the Microsoft Store.  Here is the link to download ubuntu
https://www.microsoft.com/en-us/p/ubuntu/9nblggh4msv6#activetab=pivot:overviewtab
After download,
Now open Ubuntu in the Start menu or by running wsl in PowerShell or the command prompt. You'll be asked to setup a new user for Ubuntu. Remember this password as it's what you'll use later on when installing packages with sudo.

After Ubuntu installation, we need to install Ruby 2.5.0
The first step is to install some dependencies for Ruby.
sudo apt-get update
sudo apt-get install git-core curl zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev software-properties-common libffi-dev
Using rbenv 
Installing with rbenv is a simple two step process. First you install rbenv, and then ruby-build:
cd
git clone https://github.com/rbenv/rbenv.git ~/.rbenv
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init -)"' >> ~/.bashrc
exec $SHELL

git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bashrc
exec $SHELL
rbenv install 2.5.0
rbenv global 2.5.0
ruby -v // to check the version

The installation for rvm is pretty simple:
sudo apt-get install libgdbm-dev libncurses5-dev automake libtool bison libffi-dev
gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
curl -sSL https://get.rvm.io | bash -s stable
source ~/.rvm/scripts/rvm
rvm install 3.0.1
rvm use 3.0.1 --default
ruby -v
The last step is to install Bundler
gem install bundler
rbenv users need to run rbenv rehash after installing bundler.

Configuring Git
git config --global color.ui true
git config --global user.name "YOUR NAME"
git config --global user.email "YOUR@EMAIL.com"
ssh-keygen -t rsa -b 4096 -C "YOUR@EMAIL.com"
The next step is to take the newly generated SSH key and add it to your Github account. You want to copy and paste the output of the following command and click the link below 
https://github.com/settings/keys
cat ~/.ssh/id_rsa.pub
Once you've done this, you can check and see if it worked:
ssh -T git@github.com

Installing Rails

We need to install npm with node version v12.16.0
Here is the link to download
https://nodejs.org/download/release/v12.16.0/
To install NodeJS and Yarn, we're going to add it using the official repository:
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list

sudo apt update
sudo apt-get install -y nodejs yarn

gem install rails -v 6.0.2
If you're using rbenv, you'll need to run the following command to make the rails executable available:
rbenv rehash
Now that you've installed Rails, you can run the rails -v command to make sure you have everything installed correctly:
rails -v //to check the  version





