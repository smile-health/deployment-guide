# Infrastructure and Architecture Guide

## File Structure
``` bash
├── environments
│   ├── Makefile
│   ├── prod
│   │   ├── aws_backup
│   │   │   └── terragrunt.hcl
│   │   ├── aws_mq
│   │   │   └── terragrunt.hcl
│   │   ├── aws_redis
│   │   │   └── terragrunt.hcl
│   │   ├── aws_secrets
│   │   │   └── terragrunt.hcl
│   │   ├── aws_waf
│   │   │   └── terragrunt.hcl
│   │   ├── buckets
│   │   │   └── terragrunt.hcl
│   │   ├── ec2
│   │   │   └── terragrunt.hcl
│   │   ├── ecr
│   │   │   └── terragrunt.hcl
│   │   ├── eks_clusters
│   │   │   └── terragrunt.hcl
│   │   ├── iam
│   │   │   └── terragrunt.hcl
│   │   ├── rds
│   │   │   └── terragrunt.hcl
│   │   ├── route53
│   │   │   └── terragrunt.hcl
│   │   ├── security_groups
│   │   │   └── terragrunt.hcl
│   │   ├── sg_rule
│   │   │   └── terragrunt.hcl
│   │   ├── terragrunt.hcl
│   │   ├── vars.yaml
│   │   └── vpc
│   │       └── terragrunt.hcl
│   ├── tfsec-reports
│   └── uat
│       ├── aws_backup
│       │   ├── terraform.tfvars.json
│       │   └── terragrunt.hcl
│       ├── aws_mq
│       │   └── terragrunt.hcl
│       ├── aws_redis
│       │   └── terragrunt.hcl
│       ├── aws_secrets
│       │   └── terragrunt.hcl
│       ├── aws_waf
│       │   └── terragrunt.hcl
│       ├── buckets
│       │   └── terragrunt.hcl
│       ├── ec2
│       │   └── terragrunt.hcl
│       ├── ecr
│       │   └── terragrunt.hcl
│       ├── eks_clusters
│       │   └── terragrunt.hcl
│       ├── iam
│       │   └── terragrunt.hcl
│       ├── Makefile
│       ├── rds
│       │   └── terragrunt.hcl
│       ├── route53
│       │   └── terragrunt.hcl
│       ├── security_groups
│       │   └── terragrunt.hcl
│       ├── sg_rule
│       │   └── terragrunt.hcl
│       ├── terragrunt.hcl
│       ├── vars.yaml
│       └── vpc
│           └── terragrunt.hcl
```
## Application Structure
``` bash
project-root/
├── backend/
│   ├── src/
│   ├── config/
│   └── package.json
├── frontend/
│   ├── public/
│   ├── src/
│   └── package.json
├── mobile/
│   ├── assets/
│   ├── src/
│   └── app.json
├── keycloak/
│   └── realm-export.json
├── scripts/
│   ├── deploy.sh
│   └── migrate.sql
├── .env.example
├── docker-compose.yml
├── README.md
└── INSTALLATION.md
```
Notes:
- backend/: Contains the core logic, API routes, and service configurations.
- frontend/: Holds the React-based frontend app; needs to be built and served.
- mobile/: React Native mobile app for Android/iOS deployment via Expo or native builds.
- keycloak/: Used to configure Keycloak with pre-defined users, roles, and clients.
- scripts/: Includes reusable scripts for database migration, deployment, or seeding.
- .env.example: Use this file as a starting point to create your own .env configuration file.
- docker-compose.yml: Simplifies the setup process using containers (if Docker is preferred).

## Helm Chart Structure
``` bash
templates/
- deployment.yaml
- service.yaml
- hpa.yaml
- _helpers.tpl

Chart.yaml  
values.yaml
```

## Monitoring & Backup

- RDS Monitoring: Enhanced monitoring enabled (30-second intervals)
- Log Management: VPC flow logs stored in dedicated S3 bucket
- Backup Plan: Daily backups with 7-day retention

## Backup & Disaster Recovery

- Backup service utilises the Amazon Backup service from AWS;
- Backups will be conducted across all three branches (dev, staging, and production) that were created via Terraform;
- Backups are targeted based on the resource tag on Terraform;
- Backups are scheduled to run daily at 03:00 WIB or 20:00 UTC;
- Backup retention policy period will store the backed-up data for 7 days.
