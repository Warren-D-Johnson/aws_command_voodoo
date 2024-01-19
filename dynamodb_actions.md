### DynamoDB AWS CLI

*Scan operation to export all records from a table*<br>
```aws dynamodb scan --table-name TABLE_NAME_HERE > export.json```<br>
<br>
*Get an item by primary key*<br>
```aws dynamodb get-item --table-name TABLE_NAME_HERE --key '{"uuid": {"S":"e92ee667-db5b-4068-b8c6-2a039ffce102"}}'```<br>
<br>
*Update a table record by specifying key and attributes*<br>
```aws dynamodb update-item --table-name "TABLE_NAME_HERE" --key '{"uuid": {"S": "e92ee667-db5b-4068-b8c6-2a039ffce102"}}' --attribute-updates '{"last_good": {"Value": {"N": "23"},"Action": "PUT"}}' --return-values UPDATED_NEW```<br>
<br>
*Delete a record by primary key*<br>
```aws dynamodb delete-item --table-name "TABLE_NAME_HERE" --key '{"uuid": {"S": "e92ee667-db5b-4068-b8c6-2a039ffce102"}}'```<br>
<br>
*Enable point-in-time recovery for a table*<br>
```aws dynamodb update-continuous-backups --table-name "TABLE_NAME_HERE" --point-in-time-recovery-specification PointInTimeRecoveryEnabled=true```<br>
<br>
*Loop through all tables in a region and enable point-in-time backup*<br>
```for table_name in $(aws dynamodb list-tables --query 'TableNames[]' --output text); do aws dynamodb update-continuous-backups --table-name $table_name --point-in-time-recovery-specification PointInTimeRecoveryEnabled=true; done```<br>
<br>
*List DynamoDB tables in a region and output the names in alphabetical order*<br>
```aws dynamodb list-tables --region ap-southeast-1 --output text | sed 's/TABLENAMES//g' | sed 's/\s//g' | sort -f```<br>
<br>

