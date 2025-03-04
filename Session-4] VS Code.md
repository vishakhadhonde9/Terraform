## Download and Install Terraform
- Go to the Terraform official website:

       https://developer.hashicorp.com/terraform/downloads
  
- Download the Windows version (.zip file).
- Extract the .zip file to a folder (e.g., C:\Terraform).
- Add this folder to the System PATH:
    - Press Win + R, type sysdm.cpl, and press Enter.
- Go to the Advanced tab → Click Environment Variables.
- Find Path under System Variables, select it, and click Edit.
- Click New and add: C:\Terraform
- Click OK → OK → OK.

## Verify Installation

    terraform -version

If installed correctly, it will show the Terraform version.

## Create a Terraform Configuration File
Open Notepad or VS Code and create a file named main.tf.

        provider "aws" {
          region = "us-east-1"
        }
        
        resource "aws_s3_bucket" "my_bucket" {
          bucket = "my-unique-bucket-name-12345"
        }


- Save the file in a folder (e.g., C:\TerraformProject).

## Initialize Terraform

      cd C:\TerraformProject
      
      terraform init

      
## Plan and Apply

    terraform plan
    terraform apply


# Destroy (Optional)
    
    terraform destroy
