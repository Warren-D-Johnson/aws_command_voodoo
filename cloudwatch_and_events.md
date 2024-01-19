### Cloudwatch and Event Bridge AWS CLI

*For a specific time period, get lambda execution duration in GB/s*<br>
```aws cloudwatch get-metric-statistics --namespace AWS/Lambda --metric-name Duration --dimensions Name=FunctionName,Value=MY_LAMBDA_FUNCTION --statistics Sum --start-time 2023-01-01T00:00:00Z --end-time 2023-01-31T23:59:59Z --period 86400 | jq '.Datapoints | map(.Sum) | add'```<br>
<br>
*Searching a Cloudwatch group for a specific filter pattern in a specific time frame*<br>
```aws logs filter-log-events  --start-time `date -d 2021-11-30T00:00:00Z +%s`000 --end-time `date -d 2021-11-30T23:59:59Z +%s`000   --log-group-name /aws/lambda/LOG_GROUP_NAME_HERE --filter-pattern Paddington```<br>
<br>
