# Cloud Cheat Sheet

## Service models

| Model | You manage | Provider manages | Example |
|---|---|---|---|
| IaaS | OS, runtime, app, data | Hardware, network, virtualization | EC2, Azure VM |
| PaaS | App, data | OS, runtime, scaling | Elastic Beanstalk, App Service |
| SaaS | Usage only | Everything | Gmail, Microsoft 365 |
| FaaS | Function code | Servers, scaling | Lambda, Azure Functions |

## Deployment models

| Model | Meaning |
|---|---|
| Public | Shared provider infrastructure |
| Private | Dedicated to one org |
| Hybrid | Public + private connected |
| Multi-cloud | Multiple providers |

## Key terms

| Term | Meaning |
|---|---|
| Region | Geographic area with data centers |
| Availability Zone (AZ) | Isolated data center(s) inside region |
| Scalability | Add capacity: vertical (bigger), horizontal (more) |
| Elasticity | Auto scale up/down with load |
| High availability | Survives component failure |
| Fault tolerance | Zero downtime on failure |
| Pay-as-you-go | Billed per use |
| CapEx → OpEx | Upfront hardware → monthly bill |

## Service mapping

| Category | AWS | Azure | GCP |
|---|---|---|---|
| VM | EC2 | Virtual Machines | Compute Engine |
| Serverless | Lambda | Functions | Cloud Functions |
| Containers (managed K8s) | EKS | AKS | GKE |
| Containers (simple) | ECS / Fargate | Container Apps | Cloud Run |
| PaaS web | Elastic Beanstalk | App Service | App Engine |
| Object storage | S3 | Blob Storage | Cloud Storage |
| Block storage | EBS | Managed Disks | Persistent Disk |
| File storage | EFS | Azure Files | Filestore |
| SQL DB | RDS / Aurora | Azure SQL | Cloud SQL |
| NoSQL | DynamoDB | Cosmos DB | Firestore |
| Network | VPC | VNet | VPC |
| DNS | Route 53 | Azure DNS | Cloud DNS |
| CDN | CloudFront | Front Door / CDN | Cloud CDN |
| Identity | IAM | Entra ID + RBAC | IAM |
| Secrets | Secrets Manager | Key Vault | Secret Manager |
| Monitoring | CloudWatch | Monitor | Cloud Monitoring |
| Queue | SQS | Service Bus / Queue Storage | Pub/Sub |
| IaC | CloudFormation | ARM / Bicep | Deployment Manager |
| CLI | `aws` | `az` | `gcloud` |
