---
title: Homebrew Installed Version
parent: Code
layout: default
---




# Homebrew Installed Version

<br>
This is a simple one-liner to return the `brew` version installed on macOS.

This allows for reporting of how many users have brew installed and what versions they are running.

<br>
```shell
$(which brew 2> /dev/null)  --version 2> /dev/null | awk '{print $2}' | xargs

#output
4.4.26
```
<br>


Rolling this into a Jamf extension attribute makes it even easier to report via smart groups.


<br>
```bash
#!/bin/zsh

################################################################################
# Name      	: homebrew_version_ea.sh
# Date          : 2025.01.28
# Version       : 0.1.0
# Author       	: Nic Scott
# Email         : nls.inbox@gmail.com
# Description	: checks to see if homebrew is installed and reports version
################################################################################

## VARIABLES -------------------------------------------------------------------
homebrew_path=$(which brew 2> /dev/null )
homebrew_version=$($homebrew_path --version 2> /dev/null | awk '{print $2}' | xargs)

## FUNCTIONS -------------------------------------------------------------------
function check_homebrew_version () {
    if [[ -z $homebrew_version ]]; then
        echo "<result>"Not Installed"</result>"
    else
        echo "<result>"$homebrew_version"</result>"
    fi
}

## COMMANDS --------------------------------------------------------------------
check_homebrew_version
```


<br>
Example output:

```bash
<result>4.4.26</result>
```

