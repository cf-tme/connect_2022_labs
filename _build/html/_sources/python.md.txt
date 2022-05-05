# Setup Python 
Python will be used in Lab 2 to make API calls to Cloudflare
## MacOS
**Install Homebrew:**

The fastest way to install packages onto MacOS is with Homebrew, if you already have Homebrew installed you can skip this step

To install Brew, in a terminal window enter

``` sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

**Install Python3:**

In a terminal window enter:

``` sh
brew install python
```
## Linux

Installation of Python3 can be done with the built in package managers on most all linux distributions - to cover common use cases the steps below are for Debian and CentOS

**Debian, Ubuntu Linux, Raspberry Pi OS (apt)**

Python 3 may already be installed on your distribution if not run:

``` sh
sudo apt-get install python3
```

**Fedora, CentOS, Red Hat Enterprise Linux (dnf)**

``` sh
sudo dnf install python3
```

## Windows

Installation of Python3 can be done with powershell winget package manager. Open PowerShell and enter the following installation command:

``` sh
winget install -e --id Python.Python.3
```

If prompted enter *Y* to approve installation

Once installation is complete you must add Python3 installation to the Windows PATH:

```sh
$Env:PATH += ";%userprofile%\AppData\Local\Programs\Python\Python310"
```

```{admonition} Python 3 Setup Complete! 
:class: note
You have successfully setup Python! Lets Get Started with the Labs!
```