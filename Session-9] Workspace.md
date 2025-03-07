# Workspace -
- Workspaces enable you to manage multiple instances or resources of your infrastructure using the same configuration.
- Terraform starts with a single workspace named “default”.
- The workspace feature of Terraform allows users to switch between multiple instances of a single configuration with a unique state file.
- For local states, Terraform stores the workspace states in a directory called terraform.tfstate.d.


## Workspace commands -
- **terraform workspace new <workspace_name>** --> command is used to create a new workspace and switched to a new workspace.
- **terraform workspace list** --> command is used to list all existing workspaces.
- **terraform workspace select <workspace_name>** --> command is used to choose a different workspace to use for further operations.
- **terraform workspace delete <workspace_name>** --> command is used to delete an existing workspace.
- **terraform workspace show** --> command is used to output the current workspace.

## Directory -
        terraform-workspace-ec2/
        │── main.tf
        │── variables.tf
        

### main.tf -


        provider "aws" {
          region = "us-east-1"  # Change this if needed
        }
        
        # Select instance type based on workspace
        locals {
          instance_type = terraform.workspace == "prod" ? var.instance_type_prod : var.instance_type_dev
        }
        
        resource "aws_instance" "example" {
          ami           = "ami-0c55b159cbfafe1f0"  # Amazon Linux 2 AMI (change if needed)
          instance_type = local.instance_type
        
          tags = {
            Name        = "${var.project_name}-${terraform.workspace}"
            Environment = terraform.workspace
            InstanceType = local.instance_type
          }
        }
        
            


### variable.tf -

variable "project_name" {
  description = "Project name prefix for EC2 instance"
  default     = "workspace-demo"
}

variable "instance_type_dev" {
  description = "EC2 instance type for dev"
  default     = "t2.micro"
}

variable "instance_type_prod" {
  description = "EC2 instance type for production"
  default     = "t3.medium"
}





### Commands -

- **dev Workspace-**

  - terraform init
  - terraform workspace new dev
  - terraform workspace show  
  - terraform apply 


- **prod Workspace-**

  - terraform init
  - terraform workspace new prod
  - terraform workspace show  
  - terraform apply 






















