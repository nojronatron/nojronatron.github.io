# Notes Taken While Setting Up My Workstation for 301

## Why Brew

The claim is instaling Brew makes installation of other packages easier.  
Ran into issues with ZSH, NodeJS, NPM, and ESLint.  
It is wholly possible that there was a bit of a cascading effect (one failure let to others in non-obivous ways).  
I managed to work-around all issues by following these strategies:  

1. Restarting ZSH (shell) after making any changes that impact path or '.zshconf'.  
2. Prefixing install or update commands with sudo when a warning or error message indicates the 'OS is not allowing access to 9files'.  

I also took it upon myself to skip using Brew altogether after it couldn't install NPM properly:  

1. Installing Node Package Manager (NPM) using `npm install -g npm`.  
2. Updating Node Version Manager (NVM) using `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash`.  
3. Updating Node to the latest version using NVM: ___.  

## MongoDB

Installing MongoDB is fairly straightforward, following the MSFT WSL Documentation.

*Remember*: When asked to auto start MongoD using systemctl, instead do this: `sudo /etc/init.d/*`  

Example: When asked to do `sudo systemctl status docker`  
...instead do `/etc/init.d/docket status` or `sudo service docker status`  

### MongoDB Start Stop Status

Follow the MSFT WSL documents on installing and configurating MongoDB, then:  

- sudo service mongod start  
- sudo service mongod status  
- sudo service mongod stop  

### MongoDB Diagnostic

`mongo --eval 'db.runCommand({ connectionStatus: 1})'`  

### MongoDB and VSCode

Look for the Azure CosmosDB extension.  

### Mongo Client

`mongo`  

## Data Structures and Algorithms

TODO: Come back to this when a template repo is available (probably via Canvas, Syllabus).  

### ESLinter

When creating React applications, eslint is already included, so if you've created one already, rm it.  

## Footer

Go back to [Readme.md](../README.html)  
