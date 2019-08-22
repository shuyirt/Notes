# AWS CLI 

## Installation for MacOS

### Install Python3 

### Install AWS CLI

1. Choose the install AWSCLI using PIP

   Please using python3 and pip3

    https://docs.aws.amazon.com/cli/latest/userguide/cli-install-macos.html

2. if you run `aws —version`, it shows `command not found`, try to see if your aws is installed under `~/Library/Python/3.7/bin/`. If it is, you can run 

```BASH
cd ~
sudo nano .bash_profile

# add follow line to your .bash_profile file and save
export PATH=~/Library/Python/3.7/bin/:$PATH
```


