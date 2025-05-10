---
title: Salesforce Exported Reports
parent: Code
layout: default

---




# Salesforce Exported Reports With Sumo Logic Query

<br>
Salesforce falls under specific audit and compliance rules for our company. A major effort has gone into ingesting Event Monitoring logs into Sumo Logic and building Dashboards and reports.

A blind spot we've had in the past is, "who downloaded what report?"

The event data and the report name are in different tables in the Event Monitoring logs. Heres an example of a table join to connect the user with the report exported.
<br>

{: .custom }
> **Note**: This requires you have a subscription to Event Monitoring

<br>
<p align="center" width="100%">
    <img width="100%" src="/site/images/salesforce-reports.png">
    <figcaption align="center" style="font-size:12px;"> Example output (names and reports removed) </figcaption>
</p>
<br>




## Sumo Logic Query

```sql
_sourceCategory="salesforce" 
    | JSON "REPORT_DESCRIPTION", "EVENT_TYPE", "REQUEST_ID" NODROP
    | JOIN
        ( WHERE EVENT_TYPE = "Report"
            | JSON "REPORT_ID_DERIVED_LOOKUP" as REPORT_NAME NODROP) as report,
        ( WHERE EVENT_TYPE = "ReportExport"
            | JSON "TIMESTAMP_DERIVED" as TIMESTAMP NODROP
            | JSON "CLIENT_IP" AS CLIENT_IP NODROP
            | JSON "CLIENT_INFO" AS CLIENT_AGENT NODROP
            | JSON "USER_ID_DERIVED_LOOKUP" AS User NODROP) as export
    on report.REQUEST_ID = export.REQUEST_ID
    | COUNT export_TIMESTAMP, export_User, export_CLIENT_IP, 
        export_CLIENT_AGENT, report_REPORT_NAME
```
<br>

You can create queries directly in Sumo Logic, and it's very forgiving of white space and indetns with syntax.

I prefer to write and format queries in VS Code with the [sumo-logic-highlight](https://marketplace.visualstudio.com/items?itemName=NicScott.sumo-logic-highlight), before I copy to Sumo Logic. It's a simple language syntax I created to add keyword highlighting.



