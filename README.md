# AzureSentinelQueries
A collection of useful KQL queries and links to the source for Azure Sentinel

## Azure Security Center Alert Queries
https://azsec.azurewebsites.net/2019/11/29/work-with-azure-security-center-alert-in-log-analytics/

Count the total number of alerts for the past 24 hours
```
SecurityAlert
| where TimeGenerated >=ago(24h)
| count
```

List Specific Alert Types and show the columns TimeGenerated, StartTime, EndTime, and ResourceId
```
SecurityAlert
| where TimeGenerated >=ago(24h)
| where AlertName == "Traffic from unrecommended IP addresses was detected"
| project TimeGenerated, StartTime, EndTime, ResourceId
```

Count the number of alerts for each point of time and sort by descending number
```
SecurityAlert
| where TimeGenerated >=ago(24h)
| summarize count() by TimeGenerated
| sort by count_
```

Count the number of alerts that occurred every hour during the last 24 hours
```
SecurityAlert
| where TimeGenerated >=ago(24h)
| summarize count() by bin(TimeGenerated, 1h)
```
