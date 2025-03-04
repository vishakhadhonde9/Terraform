# Providers -
- A provider in Terraform is a plugin that allows Terraform to interact with different cloud platforms (e.g., AWS, Azure, GCP).
- Terraform uses providers to manage and provision resources in the cloud or other services.
- Each Terraform configuration file must define the required provider.

        provider "aws" {
          region  = "us-east-1"
        }



| **Cloud Provider**  | **Terraform Provider**          | **Provider Source**                 |
|--------------------|--------------------------------|-------------------------------------|
| AWS              | `aws`                          | `hashicorp/aws`                    |
| Microsoft Azure  | `azurerm`                      | `hashicorp/azurerm`                |
| Google Cloud     | `google`                       | `hashicorp/google`                 |


# Provider Versioning

                terraform {
                  required_providers {
                    aws = {
                      source  = "hashicorp/aws"
                      version = "~> 5.0"
                    }
                  }
                }



# Resources -
- A resource is a cloud infrastructure component created by Terraform.
- Examples of resources:
   - EC2 instances
   - S3 buckets
   - VPCs
   - IAM users
   - Declaring a Resource


                resource "aws_instance" "block_name" {
                  ami           = "ami-12345678"
                  instance_type = "t2.micro"
                }



