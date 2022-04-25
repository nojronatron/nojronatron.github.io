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

See the instructions in the class repo for specifics.  

Overview:

1. CD into the correct folder.  
2. Check out a new local branch.  
3. Get the Challenge code by running an sh script.  
4. Execute `npm test` to see test results for all tests in the designated code file.  
5. ACP to GH then wait a minute for GH Action to finish.  
6. Check the Actions tab to confirm tests are passing.  
7. PR to main an submit assignment.  

### ESLinter

When creating React applications, eslint is already included, so if you've created one already, rm it.  

### Setup GPG and Pass

1. Go to [PasswordStore.org](https://www.passwordstore.org/) and follow the steps to install 'pass', it will be needed later.  
2. Review steps in GitHub Credential Manager [docs](https://github.com/GitCredentialManager/git-credential-manager/blob/main/docs/credstores.md)  
3. Ensure GPG is installed and version is gt 2.1.17
4. Follow steps in github docs [here](https://docs.github.com/en/github-ae@latest/authentication/managing-commit-signature-verification/generating-a-new-gpg-key)  
5. The GPG User ID is the long string of your username comment and email address.  
6. Use GPG Armor to create the signed key.  
7. Set up pass (see steps in step 1, above) to store the GPG key by User ID.  
8. Go to GitHub, Settings, SSH and GPG Keys, and upload the signed key to a new GPG key.  

*Note*: Yes, I know this is documented elsewhere for the CF classes, but the inner workings are buried in a script and I just wanted to know what was going on.  

### Git and Credential Manager

GitHub authentication no longer supports https fetch/push operations using un+pw authentication.  
Appropriate solution is to install GH Credential Manager.  
See these steps [here](https://github.com/GitCredentialManager/git-credential-manager#linux-install-instructions)  

*Note*! The link above contains an *experimental script*. Be certain that is what you want to use rather than the Ubuntu/Debian distribution instructions!!  

## Other Stuff To Consider

[Oh my Posh](https://medium.com/analytics-vidhya/customize-your-windows-powershell-with-oh-my-posh-posh-git-93284b2749b6)  

## Footer

Go back to [Readme.md](../README.html)  
