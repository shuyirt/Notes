# Node

## Installation Guide

### Using nvm

nvm is the Node Version Manager

1. your system might have `.bash_profile` file , we can just create one

`touch ~/.bash_profile`

2. restart your terminal

3. To **install** or **update** nvm, you can use the [install script](https://github.com/nvm-sh/nvm/blob/v0.34.0/install.sh) using cURL:

`curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | bash`

4. might ned to run

```
export NVM_DIR="${XDG_CONFIG_HOME/:-$HOME/.}nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
```

5. verify your installation 

`command -v nvm`

it should show `nvm`

6. install node

`nvm install node`

7. use node 

`nvm use node`

8. you can also add a `.nvmrc` file in your project

`$ echo "node" > .nvmrc`

run this in your local directory