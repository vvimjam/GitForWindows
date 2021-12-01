# Setup git on windows

#### Set home directory [Optional]
* Open ```C:\Program Files (x86)\Git\etc\profile``` file and define home directory as ``` HOME=/c/myprojects/``` anywhere at the top of the file.
* Restart Git bash
* This will not only set home directory but one can simply navigate to home directory using "cd ~"
* ###### Note: 
    If multiple users exist then it is better to set the home directory dynamically rater than globally in profile file

#### Set account details
These details will be utilized when making code commits
``` 
git config --global user.email "git email"
git config --global user.name "account name/user name"
```

#### Set up authentication
* Generate new ssh key for git account. ``` ssh-keygen -t rsa -b 4096 -C "git email" ```
    * When prompted for .ssh key save location save it at either default location or choose newly set home directory. By default key will not be saved to home directory.
* Enter pass passphrase (optional)
* Start ssh-agent  ```eval $(ssh-agent -s)```
* Add ssh key to ssh-agent [Point to ssh key directory]
 ```ssh-add ~/.ssh/id_rsa```
* Copy the contents of id_rsa.pub file (ssh key)
* Go to github > setting > SSH and PGP Keys > paste the ssh key and save


#### Assign global gitignore file
Settng up a global gitignore file is a good practice, each repo can have its own .gitignore file which would override the global config.
* Create a gitignore file in home dir ```touch ~/.gitignore```
* Open gitignore file & prepare an abstract version of the file contents.
* Set git ignore file in global config  ```git config --global core.excludesfile '~/.gitignore'```

#### Auto launching ssh-agent
* Create .bashrc file which is ready by git bash upon start  ```touch ~/.bashrc```
* Go to [launcng ssh agent on git for windows](https://help.github.com/en/github/authenticating-to-github/working-with-ssh-key-passphrases#auto-launching-ssh-agent-on-git-for-windows) and copy paste the startup script into the .bashrc file and save. 
* Ensure the env path within the script in .bashrc matches the local ssh key path.
* Restart git bash
* A waring will be shown about incorrect setup & .bash_profile file will be created. If you see an error about path not found then ensure the path shown in cmd & the first line in .bashrc is valid (env=/c/Users/PC/.ssh/agent.env).
* Enter passphrase if required
* Identity will be added to ssh-agent [key added]
* ssh-agent will start running automatically now

###### Note: To verify if ssh-agent is unning a quick peek at task manager process or "ps -p $SSH_AGENT_PID" command should give the PID of the process. If you do not see PID then ssh-agent is not running.
