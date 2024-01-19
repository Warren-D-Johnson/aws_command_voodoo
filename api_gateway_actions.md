### API Gateway Actions AWS CLI

*List API Gateway Routes without method*<br>
```aws apigatewayv2 get-routes --api-id API_ID_HERE | grep RouteKey | cut -d '"' -f 4 | cut -d ' ' -f 2-```<br>
<br>
*List all API Gateways along with their ids*<br>
```aws apigatewayv2 get-apis --query 'Items[*].{Name:Name,ApiId:ApiId}' --output text```<br>
<br>
