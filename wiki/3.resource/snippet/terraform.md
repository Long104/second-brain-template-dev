---
title: "Terraform Snippets"
aliases:
  - "terraform hcl"
tags:
  - para/resource
  - topic/terraform
  - status/active
created: 2026-06-09T14:39:00Z
updated: 2026-06-09T14:39:00Z
type: "snippet"
id: "202606091439"
source: ""
---

# Terraform Snippets

> Reusable Terraform HCL config patterns.

---

## Basics

### Snippet: Provider Setup

| Field       | Value                            |
| ----------- | -------------------------------- |
| Description | Standard provider + remote state |
| When to use | Every Terraform project          |

```hcl
terraform {
  required_version = ">= 1.5"
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
  backend "s3" {
    bucket = "my-tfstate"
    key    = "prod/terraform.tfstate"
    region = "ap-southeast-1"
  }
}

provider "aws" {
  region = "ap-southeast-1"
}
```

### Snippet: EC2 Instance

```hcl
resource "aws_instance" "web" {
  ami                    = "ami-0c55b159cbfafe1f0"
  instance_type          = "t3.micro"
  subnet_id              = aws_subnet.main.id
  vpc_security_group_ids = [aws_security_group.web.id]

  root_block_device {
    volume_size = 30
    volume_type = "gp3"
  }

  tags = {
    Name = "web-server"
  }
}
```

### Snippet: S3 Bucket

```hcl
resource "aws_s3_bucket" "assets" {
  bucket = "myapp-assets-prod"
}

resource "aws_s3_bucket_public_access_block" "assets" {
  bucket = aws_s3_bucket.assets.id

  block_public_acls       = true
  block_public_policy     = true
  ignore_public_acls      = true
  restrict_public_buckets = true
}

resource "aws_s3_bucket_versioning" "assets" {
  bucket = aws_s3_bucket.assets.id
  versioning_configuration {
    status = "Enabled"
  }
}
```

---

## Patterns

### Pattern: VPC with Subnets

```hcl
resource "aws_vpc" "main" {
  cidr_block           = "10.0.0.0/16"
  enable_dns_hostnames = true
  enable_dns_support   = true
  tags = { Name = "main" }
}

resource "aws_subnet" "public" {
  count                   = 2
  vpc_id                  = aws_vpc.main.id
  cidr_block              = cidrsubnet(aws_vpc.main.cidr_block, 8, count.index)
  availability_zone       = data.aws_availability_zones.available.names[count.index]
  map_public_ip_on_launch = true
  tags = { Name = "public-${count.index}" }
}

resource "aws_subnet" "private" {
  count             = 2
  vpc_id            = aws_vpc.main.id
  cidr_block        = cidrsubnet(aws_vpc.main.cidr_block, 8, count.index + 2)
  availability_zone = data.aws_availability_zones.available.names[count.index]
  tags = { Name = "private-${count.index}" }
}
```

### Pattern: RDS Postgres

```hcl
resource "aws_db_instance" "main" {
  identifier     = "mydb"
  engine         = "postgres"
  engine_version = "16"
  instance_class = "db.t4g.micro"
  allocated_storage = 20

  db_name  = "myapp"
  username = "admin"
  password = var.db_password

  vpc_security_group_ids = [aws_security_group.rds.id]
  db_subnet_group_name   = aws_db_subnet_group.main.name

  backup_retention_period = 7
  backup_window           = "03:00-04:00"
  maintenance_window      = "sun:04:00-sun:05:00"

  skip_final_snapshot = false
  final_snapshot_identifier = "mydb-final-${formatdate("YYYY-MM-DD-hhmm", timestamp())}"

  tags = { Name = "mydb" }
}
```

---

## Gotchas

| Issue                         | Cause              | Fix                                                |
| ----------------------------- | ------------------ | -------------------------------------------------- |
| State file contains secrets   | Plaintext in state | Use `sensitive = true` + state storage encryption  |
| Destroy fails on non-empty S3 | Bucket has objects | `force_destroy = true` or empty bucket first       |
| Count index changes           | Destroys/recreates | Use `for_each` with stable keys instead of `count` |
| Provider version mismatch     | Breaking changes   | Pin `~> x.y` instead of `>= x`                     |

---

## References

- [Terraform registry](https://registry.terraform.io/)
