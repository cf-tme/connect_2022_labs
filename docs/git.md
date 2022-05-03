# Setup Git 
## MacOS
**Install Homebrew:**

The fastest way to install packages onto MacOS is with Homebrew, if you already have Homebrew installed you can skip this step

To install Brew, in a terminal window enter

``` sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

**Install GIT:**

In a terminal window enter:

``` sh
brew install git
```
## Linux

Installation of Git can be done with the built in package managers on most all linux distributions - to cover common use cases the steps below are for Debian and CentOS

**Debian, Ubuntu Linux, Raspberry Pi OS (apt)**
``` sh
apt-get install git
```
**Fedora, CentOS, Red Hat Enterprise Linux (dnf)**

``` sh
dnf install git
```

## Windows

Installation of Git can be done with powershell winget package manager. Open PowerShell and enter the following installation command:

``` sh
winget install -e --id Git.Git
```

If prompted enter *Y* to approve installation

Once installation is complete you must add Git CLI installation to the Windows PATH:

```sh
$Env:PATH += ";C:\Program Files\Git\bin"
```

```{admonition} Git Setup Complete! 
:class: note
You have successfully setup GitHub CLI! Lets Get Started with the Labs!
```
