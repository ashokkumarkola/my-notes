# AWS Cheat Sheet

## Core services

| Service | Use |
|---|---|
| EC2 | Virtual servers |
| S3 | Object storage (buckets) |
| EBS | Disks for EC2 |
| VPC | Private network |
| IAM | Users, roles, policies |
| RDS | Managed SQL DB |
| DynamoDB | NoSQL key-value |
| Lambda | Serverless functions |
| ECS / EKS | Containers / Kubernetes |
| CloudWatch | Logs, metrics, alarms |
| Route 53 | DNS |
| CloudFront | CDN |
| SQS / SNS | Queue / pub-sub |

## CLI setup

```bash
aws --version
aws configure                       # key, secret, region, output
aws configure --profile work        # named profile
export AWS_PROFILE=work             # use profile
aws sts get-caller-identity         # who am I
```

Config files: `~/.aws/credentials`, `~/.aws/config`.

## S3

```bash
aws s3 ls                                  # list buckets
aws s3 ls s3://bucket/path/                # list objects
aws s3 mb s3://bucket                      # make bucket
aws s3 cp file.txt s3://bucket/            # upload
aws s3 cp s3://bucket/file.txt .           # download
aws s3 sync ./dir s3://bucket/dir          # sync folder
aws s3 rm s3://bucket/file.txt             # delete object
aws s3 rb s3://bucket --force              # delete bucket + contents
```

## EC2

```bash
aws ec2 describe-instances \
  --query 'Reservations[].Instances[].[InstanceId,State.Name,PublicIpAddress]' \
  --output table
aws ec2 start-instances --instance-ids i-0123456789
aws ec2 stop-instances  --instance-ids i-0123456789
ssh -i key.pem ec2-user@<public-ip>        # Amazon Linux (ubuntu@ for Ubuntu)
chmod 400 key.pem                          # required key permission
```

## IAM

```bash
aws iam list-users
aws iam create-user --user-name dev1
aws iam attach-user-policy --user-name dev1 \
  --policy-arn arn:aws:iam::aws:policy/ReadOnlyAccess
```

| Term | Meaning |
|---|---|
| User | Person / app with long-term credentials |
| Group | Set of users sharing policies |
| Role | Temporary credentials, assumed by service/user |
| Policy | JSON permissions (Allow/Deny, Action, Resource) |

## Lambda + logs

```bash
aws lambda list-functions
aws lambda invoke --function-name fn out.json
aws logs tail /aws/lambda/fn --follow
```

## Output tips

```bash
--output table | json | text
--query 'Items[].Name'          # JMESPath filter
--region us-east-1
```
