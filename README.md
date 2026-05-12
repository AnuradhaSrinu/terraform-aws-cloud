# Terraform AWS Cloud Infrastructure

## 📋 Overview
Production-ready AWS cloud infrastructure built with Terraform. This project demonstrates complete infrastructure-as-code practices with modular, reusable Terraform code.

## 🎯 What This Project Includes
- **VPC (Virtual Private Cloud)** - Custom networking with public/private subnets
- **EC2 Instances** - Compute resources across multiple availability zones
- **RDS Database** - Managed relational database with automated backups
- **S3 Buckets** - Object storage with proper security and encryption
- **Security Groups** - Network firewall rules and access control
- **IAM Roles** - Identity and access management for secure permissions
- **NAT Gateway** - Secure outbound internet access for private subnets
- **Internet Gateway** - Public internet connectivity

## 🏗️ Architecture
```
┌─────────────────────────────────────┐
│         AWS Cloud                   │
├─────────────────────────────────────┤
│  Internet Gateway                   │
│         ↓                           │
│  ┌─────────────────────────────┐   │
│  │  VPC (10.0.0.0/16)         │   │
│  │  ┌──────────┬──────────┐   │   │
│  │  │ Public   │ Private  │   │   │
│  │  │ Subnet   │ Subnet   │   │   │
│  │  ├──────────┼──────────┤   │   │
│  │  │ EC2      │ RDS DB   │   │   │
│  │  │ NAT GW   │ S3       │   │   │
│  │  └──────────┴──────────┘   │   │
│  └─────────────────────────────┘   │
└─────────────────────────────────────┘
```

## 📁 Project Structure
```
terraform-aws-cloud/
├── main.tf              # Main infrastructure configuration
├── variables.tf         # Variable definitions
├── outputs.tf           # Output values (IDs, endpoints, etc.)
├── vpc.tf              # VPC, subnets, gateways
├── compute.tf          # EC2 instances
├── database.tf         # RDS database
├── storage.tf          # S3 buckets
├── security.tf         # Security groups, IAM roles
├── terraform.tfvars    # Variable values (create this)
├── .gitignore          # Ignore Terraform files
└── README.md           # This file
```

## 🚀 Quick Start

### Prerequisites
```bash
# Install Terraform
brew install terraform  # macOS
# OR download from https://www.terraform.io/downloads

# Install AWS CLI
brew install awscli

# Configure AWS credentials
aws configure
# Enter your AWS Access Key ID and Secret Access Key
```

### Deployment Steps

1. **Clone this repository**
```bash
git clone https://github.com/AnuradhaSrinu/terraform-aws-cloud.git
cd terraform-aws-cloud
```

2. **Initialize Terraform** (downloads required plugins)
```bash
terraform init
```

3. **Review the plan** (see what will be created)
```bash
terraform plan
```

4. **Apply the configuration** (creates AWS resources)
```bash
terraform apply
```

5. **Confirm when prompted** (type `yes`)

6. **Get your outputs**
```bash
terraform output
```

## 📊 What Gets Created

After `terraform apply`, you'll have:
- ✅ 1 VPC with custom CIDR block
- ✅ 2 Public subnets (different availability zones)
- ✅ 2 Private subnets (different availability zones)
- ✅ 1 Internet Gateway (for public internet access)
- ✅ 1 NAT Gateway (for secure private subnet access)
- ✅ 2 EC2 instances (in public subnets)
- ✅ 1 RDS database instance (in private subnet)
- ✅ 2 S3 buckets (with encryption enabled)
- ✅ Security groups with proper firewall rules
- ✅ IAM roles and policies

## 🛠️ Configuration Options

Edit `terraform.tfvars` to customize:

```hcl
# Network Configuration
aws_region = "us-east-1"
vpc_cidr   = "10.0.0.0/16"

# Compute
instance_count = 2
instance_type  = "t3.micro"

# Database
db_instance_class = "db.t3.micro"
db_name           = "myappdb"

# Storage
enable_s3_versioning = true
enable_encryption    = true
```

## 🔐 Security Features
- ✅ Private subnets for databases (not internet-facing)
- ✅ Security groups restricting traffic
- ✅ S3 bucket encryption enabled
- ✅ IAM roles with least privilege
- ✅ RDS with automated backups
- ✅ VPC Flow Logs for monitoring

## 💰 Cost Estimation

**Monthly estimate (rough):**
- VPC + NAT Gateway: ~$30
- 2 t3.micro EC2 instances: ~$8
- RDS db.t3.micro: ~$15
- S3 storage: ~$5 (first 5GB free)
- **Total: ~$50-60/month**

**Tip:** Use `terraform destroy` to delete everything and stop costs!

## 🔄 Update/Modify

To update infrastructure:

1. **Edit the .tf files**
2. **Run `terraform plan`** (review changes)
3. **Run `terraform apply`** (apply changes)

## 📚 Key Terraform Concepts Used

| Concept | What It Does |
|---------|---|
| `resource` | Defines AWS resources (EC2, RDS, etc.) |
| `variable` | Creates customizable parameters |
| `output` | Shows important values after creation |
| `module` | Reusable configuration blocks |
| `for_each` | Create multiple resources efficiently |
| `data` | Reference existing AWS resources |

## 🧹 Cleanup

**Delete all resources (to avoid charges):**
```bash
terraform destroy
```
Type `yes` when prompted.

## ❓ Troubleshooting

**Error: "Access Denied"**
- Check AWS credentials are configured correctly
- Verify IAM user has required permissions

**Error: "VPC CIDR conflict"**
- Change `vpc_cidr` in terraform.tfvars to avoid conflicts
- Example: `10.1.0.0/16` instead of `10.0.0.0/16`

**Error: "Subnet CIDR invalid"**
- Ensure subnet CIDR is within VPC CIDR range
- Example: VPC `10.0.0.0/16` → Subnet `10.0.1.0/24`

## 📖 Learning Resources

- [Terraform AWS Provider Documentation](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)
- [AWS VPC Best Practices](https://docs.aws.amazon.com/vpc/)
- [Terraform State Management](https://www.terraform.io/docs/language/state/)

## 🤝 Contributing

Found a bug or want to improve this? Feel free to:
1. Fork this repository
2. Create a branch
3. Make your changes
4. Submit a pull request

## 📞 Contact

- **Email:** anusrig967@gmail.com
- **GitHub:** https://github.com/AnuradhaSrinu
- **LinkedIn:** [Your LinkedIn Profile]

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

---

**Built with ❤️ | Infrastructure as Code Best Practices**

