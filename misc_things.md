### Miscellaneous AWS CLI

*List Event Bridge Rules in the current region*<br>
```aws events list-rules```<br>
<br>
*List Event Bridge rules, giving us just the name in a single column*<br>
```aws events list-rules --query "Rules[].Name" --output text | tr -s '[:space:]' ' ' | tr ' ' '\n'```<br>
<br>
*Update a specific Event Bridge rule to run every five minutes*<br>
```aws events put-rule --name RULE_NAME --schedule-expression 'rate(5 minutes)' ```<br>
<br>
*Submit an AWS Transcribe job*<br>
```aws transcribe start-transcription-job --cli-input-json file://transcribe.json```<br>
```transcribe.json file: ```<br>
```{```<br>
```    "TranscriptionJobName": "8d818c1b-8975-4306-bde1-28fac6533d78",```<br>
```"LanguageCode": "en-US",```<br>
```    "Media": {```<br>
```        "MediaFileUri": "s3://mr-input-bucket/8d818c1b-8975-4306-bde1-28fac6533d78-audio.mp4"```<br>
```    },```<br>
```    "Settings":{```<br>
```    "ShowSpeakerLabels": true,```<br>
```    "MaxSpeakerLabels": 5```<br>
```    }```<br>
```}```<br>
<br>
*Calculate the byte size of an S3 bucket, recursively descending the file system tree*<br>
```aws s3 ls --summarize --human-readable --recursive s3://mr-and-mrs-bucket```<br>
<br>
*Set default region for future AWS CLI commands*<br>
```aws configure set default.region ap-east-1```<br>
<br>
*Utilize ACM to generate a certificate (automatically adds the records to Route53)*<br>
```aws acm request-certificate --domain-name *.mrfrodo.net --subject-alternative-names mrfrodo.net --validation-method DNS```<br>
<br>

