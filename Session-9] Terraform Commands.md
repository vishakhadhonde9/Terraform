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


