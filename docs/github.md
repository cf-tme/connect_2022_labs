# Setup Github
## Install Github CLI
### Linux
### MacOS
**Install Homebrew:**

The fastest way to install packages onto MacOS is with Homebrew, if you already have Homebrew installed you can skip this step

To install Brew, in a terminal window enter

``` sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Once Brew is installed you can install the Github CLI
In a terminal window enter:

``` sh
brew install gh
```

Once Github CLI is installed you can authenticate to your Github account.
In a terminal window enter:

``` sh
gh auth login
```
At the follow up prompt select *Github.com* and press enter

``` sh
? What account do you want to log into?  [Use arrows to move, type to filter]
> GitHub.com
  GitHub Enterprise Server
```

At the next prompt select *HTTPS* and press enter

``` sh
? What is your preferred protocol for Git operations?  [Use arrows to move, type to filter]
> HTTPS
  SSH
```

Enter *Y* to authenticate with GitHub credentials

``` sh
? Authenticate Git with your GitHub credentials? (Y/n)
```

Select *Login* with a web browser

``` sh
? How would you like to authenticate GitHub CLI?  [Use arrows to move, type to filter]
> Login with a web browser
  Paste an authentication token
```

Copy the provided one-time code and press *Enter* to open browser

``` sh
! First copy your one-time code: XXXX-XXXX
Press Enter to open github.com in your browser...
```

When the browser opens - Login with your Github credentials %test 

### Windows
## testing

Some **text**!
```{admonition} Here's my title
:class: warning

Here's my admonition content
```

setup gh desktop cli and git cli


```{admonition} Learn more
Visit the Brew [homepage](https://brew.sh/)
```