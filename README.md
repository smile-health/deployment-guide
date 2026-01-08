# Deployment and Installation Guide

## About

This document provides an overview of the SMILE5 application infrastructure deployed on AWS.  
The infrastructure is managed using Terragrunt and Terraform with support for multiple environments.

## Environments

| Environment | Purpose                                      | Location           |
|------------|----------------------------------------------|--------------------|
| Dev        | Developer testing, previews                  | environments/dev   |
| Staging    | User Acceptance Testing, QA, validation      | environments/uat   |
| Production | Live application                             | environments/prod  |

## Deployment Strategy

### Dev Commit
1. Developer completed the code;
2. Developer requests an Merge-Request (MR) to Dev branch;
3. System Analyst accepts the MR;
4. The code is merged with the current Dev branch code;
5. The code is deployed to the Dev environment.

### Staging Commit
1. System Analyst analyses the code stability on the Dev environment;
2. The code is stable on the Dev environment;
3. System analyst running the pipeline for deployment;
4. The code is merged with the current main/master branch code;
5. The code is deployed to the Staging environment.

### Production Commit
1. User Acceptance Testing (UAT) is conducted and approved on the Staging environment;
2. System Analyst creates tagging with pattern vX.X.X from the main/master branch;
3. The code is deployed to the Production environment.

## How It Works

### Deployment Process
1. Changes are made to the environment-specific vars.yaml file
2. Terragrunt reads the configuration and generates Terraform code
3. Terraform applies the changes to the AWS infrastructure
4. Application deployments target the provisioned infrastructure

### Configuration Management
All environment-specific settings are stored in the vars.yaml file within each environment directory. This includes:
- Network settings
- Instance types and sizes
- Security configurations
- Storage settings

## Documentation

- Deployment instructions and operational procedures are available in [Deployment & Installation Guide](DEPLOYMENT.md)
- Infrastructure architecture and structure details are available in [Infrastructure & Architecture](INFRASTRUCTURE.md)
