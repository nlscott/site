---
title: Okta User Profile
parent: Code
layout: default
---

# Okta User Profile

<br>




<br>
code
```python
#!/usr/bin/env python

import requests
import json
import os
import getpass
from datetime import datetime

## VARIBLES --------------------------------------------------------------------
currentUser = getpass.getuser()
tokenFile = f'/Users/{currentUser}/.configs/okta'
exampleURL = "https://example.okta.com"

## FUNCTIONS -------------------------------------------------------------------
def getToken():
    file = open(f'{tokenFile}')
    data = json.load(file)
    global token
    token = data["token"]
 

def getUsersGroups(userID):
    url = "{}/api/v1/users/{}/groups".format(exampleURL, userID)
    payload = {}
    headers = {
        "Accept": "application/json",
        "Content-Type": "application/json",
        "Authorization": "SSWS {}".format(token)
    }

    response = requests.request("GET", url, headers=headers, data=payload)
    results = response.json()
    
    print()
    print("Groups:")
    for x in results:
        groupName = x['profile']['name']
        print(" {}".format(groupName))
    

def getUserDetailsjson(emailAddress):
    url = "{}/api/v1/users/{}".format(exampleURL, emailAddress)
    payload = {}
    headers = {
        "Accept": "application/json",
        "Content-Type": "application/json",
        "Authorization": "SSWS {}".format(token)
    }

    response = requests.request("GET", url, headers=headers, data=payload)
    results = response.json()
    pretty_print = json.dumps(results, indent=4)

    print("Okta Profile:")
    print("  id: {}".format(results["id"]))
    print("  status: {}".format(results["status"]))
    print("  created: {}".format(results["created"]))
    print("  activated: {}".format(results["activated"]))
    print("  statusChanged: {}".format(results["statusChanged"]))
    print("  lastLogin: {}".format(results["lastLogin"]))
    print("  lastUpdated: {}".format(results["lastUpdated"]))
    print("  passwordChanged: {}".format(results["passwordChanged"]))
    print("  realmId: {}".format(results["realmId"]))
    for key, value in results["profile"].items():
        print(f"  {key}: {value}")


## COMMANDS --------------------------------------------------------------------
def main():
    getToken()
    getUserDetailsjson(emailAddress = "joe.daily@example.com")
    
if __name__ == "__main__":
    main()
```







```yaml
Okta Profile:
  id: 00u1p7f5y0pXekuwb1123x
  status: ACTIVE
  created: 2024-03-04T19:20:20.000Z
  activated: 2024-09-19T14:37:30.000Z
  statusChanged: 2024-09-19T14:39:12.000Z
  lastLogin: 2025-04-07T14:19:04.000Z
  lastUpdated: 2025-04-07T15:32:44.000Z
  passwordChanged: 2024-12-27T12:39:51.000Z
  realmId: suo1s1jzwmsXeF6TF1d8
  zipCode: 12345
  workerID: D1D23S7QJ
  employeeNumber: 101246
  workerCategoryCode: Full Time
  statuscode: A - Active
  officeLocation: Remote-US
  state: Ohio
  associateOID: W2CK8PRN9AMF6TNN
  joekName: joe
  costCenter: 049999
  shortname: joe.daily
  firstName: joe
  postalAddress: 123 Maint Street
  mobilePhone: (123) 123-1234
  departmentname: Sales
  userType: RFT
  startDate: 2024-03-31
  peopleleader: False
  lastName: daily
  gender: Male
  leaveOfAbsenceStartDate: 
  city: Springfield
  displayName: joe daily
  timezone: US/Eastern
  title: Sales
  login: joe.daily@example.com
  managerEmail: bill.manager@example.com
  countryCode: US
  department: 049999
  email: joe.daily@example.com
  hireDate: 2022-05-23
  manager: Bill Manager
  divisionname: Sales HQ
  managerId: 100182
  team: 049999
  positionStatus: Active
  organization: Example HQ
  effectiveDate: 2024-10-03
  teamname: East Coast Sales

Groups:
 Everyone
 Yubikey Required
 github-users
 App-Group-Salesforce-Users
 App-Group-Lucidchart-Licensed-Users
 NYC Users
 App-Group-Google-Enterprise-Gemini-Users
 Sales Team
 App-Group-bitwarden-SCIM-Users
 zscaler-user
```

