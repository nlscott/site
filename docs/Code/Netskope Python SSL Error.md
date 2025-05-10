---
title: Netskope Python SSL Error
parent: Code
layout: default

---


# Netskope - Python Requests CERTIFICATE_VERIFY_FAILED



<br>
## Summary: 

When running Python on Netskopeand using the `Request` module, user's receive the error message `SSL: CERTIFICATE_VERIFY_FAILED`



<p align="center" width="100%">
    <img width="100%" src="/site/images/python.png">
</p>
<br>

## Resolution:

### Option 1 - Python Import OS
Even If the Netskope Root CA cert is installed on the machine and trusted, Python request by default uses a different CA cert. The easiest solution if you’re running a direct python script is to add the 2 lines below to the top of your script. You will need the Netskope Root CA cert locally. 


Using `import os`, you can set a variable at the top of your python script. This works while on Netskope, and you can comment out when disconnected. This is very little code change or friction and can be easily turned on and off for testing. This is explicitly telling python request which cert to use for the `REQUESTS_CA_BUNDLE` call.
<br>
<br>

```python
import os 
os.environ["REQUESTS_CA_BUNDLE"] = "/opt/netskope/netskope_ca.crt"
```

 

---

### Option 2 - Export REQUESTS_CA_BUNDLE

This is a more permanent solution that sets the global variable for `REQUESTS_CA_BUNDLE` that is used by python's request module. The advantage is no code change is required, but will return an error if you are not on Netskope. 

This may not be the best solution while testing and needing to disconnect from Netskope because something is blocked or broken and you need to jump back to a previous VPN. You will have to comment and uncomment out the path in your zsh profile. Don't forget to start a new Terminal session or close your IDE and reopen to refresh your gloabl variables.
<br>
<br>


```shell
#add netskope ca to your .zshrc or .zprofile 
echo "\n\n#netskope root ca" >> ~/.zshrc 
echo "export REQUESTS_CA_BUNDLE=/opt/netskope/netskope_ca.crt" >> ~/.zshrc 
```

<br>
```shell
#verify vararible is set (new terminal session) 
echo $REQUESTS_CA_BUNDLE 

(output) /opt/netskope/netskope_ca.crt
```
