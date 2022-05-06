# Setup Node Package Manager 
npm will be used in Lab 3 to setup a local test environment to rapidly debug
## MacOS
**Install Homebrew:**

The fastest way to install packages onto MacOS is with Homebrew, if you already have Homebrew installed you can skip this step

To install Brew, in a terminal window enter

``` sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

**Install npm:**

In a terminal window enter:

``` sh
brew install node
```
## Linux

Installation of Node can be done with the built in package managers on most all linux distributions - to cover common use cases the steps below are for Debian and CentOS

**Debian, Ubuntu Linux, Raspberry Pi OS (apt)**

Node may already be installed on your distribution if not run:

``` sh
sudo apt install nodejs
sudo apt install npm
```

**Fedora, CentOS, Red Hat Enterprise Linux (dnf)**

``` sh
sudo dnf module install nodejs
```

## Windows

Installation of Node can be done with powershell winget package manager. Open PowerShell and enter the following installation command:

``` sh
winget install -e --id OpenJS.NodeJS
```

If prompted enter *Y* to approve installation

Once installation is complete you must add Python3 installation to the Windows PATH:

```sh
$Env:PATH += ";C:\Program Files\nodejs\node_modules\npm\bin"
```

```{admonition} npm Setup Complete! 
:class: note
You have successfully setup npm! Lets Get Started with the Labs!
```