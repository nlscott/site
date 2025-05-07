---
title: Setting DNS Servers On macOS
parent: Code
layout: default
---




# Setting DNS Servers On macOS

xxxxxxxxx

```bash
#!/bin/zsh

################################################################################
# Name      	: set_dns_servers.sh                                                                                                                                                 
# Date          : 2025.03.07 
# Version       : 1.0.0                                                                                    
# Author       	: Nic Scott                                               
# Email         : nls.inbox@gmail.com   
# Description	: checks to see if Wi-Fi interface is active and sets DNS Servers                                     
################################################################################


## VARIABLES -------------------------------------------------------------------
timeStampUTCOffSet=$(date +%Y-%m-%dT%H:%M:%S%z )
hostName=$(scutil --get ComputerName)
set_wifi=$(networksetup -listallnetworkservices | grep "Wi-Fi")
wifi_status="false"


## FUNCTIONS ------------------------------------------------------------------- 
function check_for_wifi () {
    if [[ "$set_wifi" = "Wi-Fi" ]]; then
        echo "${timeStampUTCOffSet} ${hostName} [INFO]  Wi-Fi: setting WiFi status to true"
        wifi_status="true"
    fi
}


function get_current_wifi_dns_servers () {
    if [[ "$wifi_status" = "true" ]]; then
        echo "${timeStampUTCOffSet} ${hostName} [INFO]  DNS Servers: getting currnet servers"
        first_dns_server=$(networksetup -getdnsservers Wi-Fi | head -n 1 | xargs)
        second_dns_server=$(networksetup -getdnsservers Wi-Fi | sed -n '2 p' | xargs)
        echo "${timeStampUTCOffSet} ${hostName} [INFO]  DNS Servers: $first_dns_server $second_dns_server"
        sleep 1
    fi
}


function update__wifi_dns_servers () {
    if [[ "$wifi_status" = "true" ]]; then
        echo "${timeStampUTCOffSet} ${hostName} [INFO]  DNS Servers: Updating DNS Servers"
        update_dns_servers=$(networksetup -setdnsservers Wi-Fi 1.1.1.1 8.8.8.8)
        first_dns_server=$(networksetup -getdnsservers Wi-Fi | head -n 1 | xargs)
        second_dns_server=$(networksetup -getdnsservers Wi-Fi | sed -n '2 p' | xargs) 
        sleep 1
        echo "${timeStampUTCOffSet} ${hostName} [INFO]  DNS Servers: Servers are updated to $first_dns_server $second_dns_server"
    fi
}


function flush_dns () {
    echo "${timeStampUTCOffSet} ${hostName} [INFO]  Clean UP: Flushing DNS cache"
    dscacheutil -flushcache
    killall -HUP mDNSResponder
}

## COMMANDS -------------------------------------------------------------------- 
check_for_wifi
get_current_wifi_dns_servers
update__wifi_dns_servers
flush_dns
```

