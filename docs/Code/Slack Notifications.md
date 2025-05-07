---
title: Slack Notifications
parent: Code
layout: default
---

# Slack Notifications

<br>



Currently working on sending notifictions to slack channels for security teams. The objective is to start with invisible events and make them visible.

This is an example of an Okta API token being creatd. Since Okta can expose a lot of PII, even if the token scope is `Read Only`. It's important to know who and for what business case a toekn is being created.


<br>
<p align="center" width="100%">
    <img width="100%" src="/images/slack.png">
    <figcaption align="center" style="font-size:12px;"> Example Slack Notification </figcaption>
</p>
<br>





## Example Webhook:
<br>

```shell
#!/bin/bash

curl -X POST "https://hooks.slack.com/services/$webhookID" \
    -d '{
    "text": "New Okta API Token Created: infrastructure.github",                             
    "blocks": [
        {
            "type": "section",
            "text": {
                "type": "mrkdwn",
                "text": "*New Okta API Token Created: `infrastructure.github`*"
            }
        },
        {
			"type": "divider"
		},
        {
            "type": "section",
            "text": {
                "type": "mrkdwn",
                "text": "*Date:* 2025-03-27\n *Token Owner:* joe.daily@example.com\n *Token Name:* infrastructure.github\n *Token ID:* 00Tx9b17c0J0UbrWe2d7\n *IP Address:* 162.10.150.14\n",
                "verbatim": true
            },
            "accessory": {
                "type": "image",
                "image_url": "https://static.stocktitan.net/company-logo/okta-lg.webp",
                "alt_text": "computer thumbnail"
            }
        },
        {
			"type": "divider"
		},
        {
			"type": "context",
			"elements": [
				{
					"type": "mrkdwn",
					"text": "*Recommendation:* If this was unexpected, contact the token owner or <slack://channel?team={workspaceID}&id={channelID}|IT> "
				}
			]
		},
        {
            "type": "context",
            "elements": [
              {
                "type": "mrkdwn",
                "text": "Source: Okta \n Debug: <https://$some-ticket-system|Ticket> | <https://$some-okta-link|Okta> | <https://some-automation-link|Tines>"
              }
            ]
        }
    ]
}'
```

