# Modules -
- Modules are containers for multiple resources that are used together.
- A module is like a blueprint for creating cloud infrastructure (like servers, databases, networking, etc.).
- Instead of writing the same Terraform code multiple times, you can write it once and reuse it as a module.

# Types of Terraform Modules -
## Root Module -
- This is the main Terraform configuration that calls other modules.
- It usually resides in the root directory of your Terraform project.

## Child Module -
- A reusable module that defines specific resources (e.g., EC2, VPC, RDS).
- Stored in a separate directory and used by the root module.

## Public Module (Terraform Registry) -
- Pre-built modules available at Terraform Registry.
- Example: terraform-aws-modules/vpc/aws provides a reusable AWS VPC module.

          
            terraform-project/
          │── terraform/               # Module Directory
          │   │── main.tf              # Defines resources
          │   │── variables.tf         # Defines input variables
          │   │── outputs.tf           # Defines output values
          │   │── terraform.tfvars     # Defines variable values
          │
          │── root/                    # Root Module (Calls the module)
          │   │── main.tf              # Calls the module
          │   │── terraform.tfvars      # Provides values for variables
          │   │── provider.tf           # Specifies cloud provider




## main.tf (Defines EC2 Instance)

          resource "aws_instance" "example" {
            ami           = var.ami_id
            instance_type = var.instance_type
          
            tags = {
              Name = "MyTerraformInstance"
            }
          }

          
## terraform/variables.tf (Defines Input Variables)

      variable "ami_id" {
        description = "AMI ID for the EC2 instance"
        type        = string
      }
      
      variable "instance_type" {
        description = "Instance type for the EC2 instance"
        type        = string
      }


## terraform/outputs.tf (Defines Output Values)

      output "instance_id" {
        description = "ID of the created EC2 instance"
        value       = aws_instance.example.id
      }
## terraform.tfvars (Defines Variable Values)

    ami_id         = "ami-12345678"
    instance_type  = "t2.micro"


# Create the Root Module (root/)
- The root module calls the EC2 module and specifies cloud providers.

## main.tf 

    provider "aws" {
      region = "us-east-1"  # Change region as needed
    }
    
    module "my_ec2" {
      source         = "../terraform"  # Path to the module
      ami_id         = var.ami_id
      instance_type  = var.instance_type
    }

 
## root/variables.tf (Define Input Variables for Root)

                    variable "ami_id" {
                      description = "AMI ID for the EC2 instance"
                      type        = string
                    }
                    
                    variable "instance_type" {
                      description = "Instance type for the EC2 instance"
                      type        = string
                    }

                    
## root/terraform.tfvars (Provide Variable Values)

                    ami_id         = "ami-12345678"
                    instance_type  = "t2.micro"













  
