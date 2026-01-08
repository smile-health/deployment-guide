# Deployment Instructions

## Prerequisites

- AWS CLI configured with appropriate credentials
- Terraform version 1.0.0 or later
- Terragrunt version 0.35.0 or later
- kubectl for interacting with Kubernetes clusters
- AWS IAM permissions to create required resources

## Initial Deployment

1. Clone the repository
2. Review and customize the environment-specific vars.yaml file
3. Initialize Terragrunt
4. Plan the deployment
5. Apply the configuration
6. Verify deployment

## Deploying Individual Components

- Deploy VPC only
- Deploy EKS clusters
- Deploy RDS instances

## Updating Existing Infrastructure

1. Pull latest changes
2. Update vars.yaml
3. Plan changes
4. Apply changes

## Destroying Infrastructure

CAUTION: This will delete all resources. Use with extreme care.

1. Plan the destruction
2. Destroy resources

## Handling Deployment Errors

1. Read error messages
2. Check AWS console
3. Run with debug logs

## Post-Deployment Configuration

1. Configure kubectl for EKS clusters
2. Verify EKS connectivity
3. Access RDS databases through bastion host
4. Set up application secrets

## Common Tasks

### Adding a New Service
1. Add required ECR repository
2. Add required secrets
3. Apply changes
4. Deploy the service

### Scaling Resources
- Update EKS or RDS parameters in vars.yaml
- Apply changes

### Accessing Resources
- Databases: Bastion host
- EKS clusters: kubectl
- Private services: Bastion host

## Notes & Recommendations

- Single NAT gateway used for UAT cost optimization
- Production should consider multi-AZ deployment
- Security groups follow least-privilege principle
- Regular IAM review is recommended
