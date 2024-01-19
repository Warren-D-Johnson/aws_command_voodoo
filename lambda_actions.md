### Lambda Functions AWS CLI

*Export environment variables and overwrite another Lambda's environment variables*<br>
1 - ```aws lambda get-function-configuration --function-name SOURCE_FUNCTION --query 'Environment.Variables' --output json > source_env.json```<br>
2 - ```echo "{\"Variables\": $(cat source_env.json)}" > formatted_source_env.json```<br>
3 - ```aws lambda update-function-configuration --function-name TARGET_FUNCTION --environment file://formatted_source_env.json```<br>
<br>
*Wait for a function to finish updating*<br>
```aws --region=us-east-1 lambda wait function-updated --function-name FUNC_E_TOWN```<br>
<br>
*One-liner to get the function package download link*<br>
```aws lambda get-function --function-name FUNKY | grep Location | awk '{$1=$1;print}' | awk '{gsub("\"Location\": \"", "", $0);print}' | awk '{gsub("\"", "", $0);print}'```<br>
<br>
*When creating a lambda from the CLI, you need to provide basic "Hello World" function code with it.<br>
Though the console automates role creation, the CLI does not so you must create the role yourself.<br>
We wait 10 seconds after role creation to ensure its consistent*<br>
```LAMBDA_NAME="name_goes_here"; AWS_REGION="us-east-1"; RANDOM_SUFFIX=$(openssl rand -hex 3); ROLE_NAME="${LAMBDA_NAME}-${RANDOM_SUFFIX}"; echo 'exports.handler = async (event, context) => { return { statusCode: 200, body: "Hello, World!" }; };' > temp.txt; zip function.zip temp.txt; aws iam create-role --region $AWS_REGION --role-name $ROLE_NAME --assume-role-policy-document '{"Version": "2012-10-17","Statement": [{"Effect": "Allow", "Principal": {"Service": "lambda.amazonaws.com"},"Action": "sts:AssumeRole"}]}'; aws iam attach-role-policy --region $AWS_REGION --role-name $ROLE_NAME --policy-arn arn:aws:iam::aws:policy/service-role/AWSLambdaBasicExecutionRole; sleep 10; ROLE_ARN=$(aws iam get-role --region $AWS_REGION --role-name $ROLE_NAME --query 'Role.Arn' --output text); aws lambda create-function --region $AWS_REGION --function-name $LAMBDA_NAME --runtime nodejs18.x --role $ROLE_ARN --handler temp.handler --zip-file fileb://function.zip; aws lambda put-function-event-invoke-config --region $AWS_REGION --function-name $LAMBDA_NAME --maximum-retry-attempts 0 --maximum-event-age-in-seconds 60; rm index.js function.zip```
<br>
<br>