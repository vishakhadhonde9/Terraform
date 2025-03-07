# Terraform Import -
- Terraform import command used to import resources to the state file.
- If you created resources outside of Terraform and now want Terraform to manage them.
- If your terraform.tfstate file is lost or deleted but your infrastructure is still running you can re-import resources to rebuild the state file.





      resource "aws_instance" "my_ec2_instance" {
        ami           = "ami-0abcdef1234567890"  # Replace with your instance's AMI ID
        instance_type = "t2.micro"              # Replace with your instance's type
        # Add other necessary configurations
      }



- terraform import aws_instance.my_ec2 i-1234567890abcdef0


      resource "aws_s3_bucket" "example" {
        bucket = "your-existing-bucket-name"
        Additional configuration can be added here
      }


- terraform import aws_s3_bucket.example your-existing-bucket-name


# Terraform Format -
- **terraform fmt** command is used to rewrite Terraform configuration files to a canonical format and style.
- This command fixes the formatting of Terraform files.
- It automatically corrects spacing, indentation, and style.





# Terraform Taint
- terraform taint command manually marks a Terraform-managed resource as tainted, forcing it to be destroyed and recreated on the 
next apply.
- This command marks a resource as "tainted", meaning Terraform will destroy and recreate it the next time you run terraform apply.
- Useful if a resource is not working properly and needs to be replaced.

            terraform taint aws_instance.example


# Terraform Untaint
- If you marked a resource as tainted by mistake, this command removes the taint so Terraform does not replace it.

            terraform untaint aws_instance.example


# Terraform Show
- The terraform show command is used to provide human-readable output from a state or plan file.
- **terraform show -json** will show a JSON representation of the plan, configuration, and current state.

# Terraform plan -destroy
- The behavior of any terraform destroy command can be previewed at any time with an equivalent terraform plan -destroy command.
- This command previews what will happen if you delete everything.

# Terraform Refresh -
- Updates Terraform’s state file with real-world changes.
- If you manually change something in AWS (or other providers), this command will sync Terraform’s state file.

# Terraform Validate -
- Checks for errors in your Terraform files before running terraform apply.
- Helps ensure that your configuration is correct and will not fail.

            terraform validate

- Use case: If you forget a closing bracket {} in main.tf, this command will catch it.

## Terraform State List -
- Lists all resources Terraform is managing in its state file.
- Helps check what Terraform knows about in the current infrastructure.

