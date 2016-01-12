
# AWS Cloudformation

## Getting the ARN for a DynamoDB table or Kinesis stream

Say we had the DynamoDB table

```json
"TableKeyHere": {
  "Type": "AWS::DynamoDB::Table",
  "Properties": {
    "TableName": "TableNameHere"
  }
}

```
 
This is how to get the ARN for it that is sensitive to the `region` and the `accountId`:

### YAML
 
```yaml
Fn::Join: [":", ["arn:aws:dynamodb", {Ref: AWS::Region}, {Ref: AWS::AccountId}, ":table/", {Ref: TableKeyHere}]] 
```

### JSON

```json
{ "Fn::Join": [":", ["arn:aws:dynamodb", {"Ref": "AWS::Region"}, {"Ref": "AWS::AccountId"}, ":table/", {"Ref": "TableKeyHere"}]]}
```

## Kinesis Stream

```json
{ "Fn::Join": [":", ["arn:aws:kinesis", {"Ref": "AWS::Region"}, {"Ref": "AWS::AccountId"}, ":stream/", {"Ref": "StreamNameHere"}]]}
```

