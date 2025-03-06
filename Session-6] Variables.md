# Variables -
- Variables are like containers that store values.
- Instead of writing a value directly, you store it in a variable and use it whenever needed.
- This makes code flexible, reusable, and easy to change.

# Types of Variable -

## 1]  Input Variables -
- Input variables allow users to pass values into Terraform configurations.

### Declear -

      variable "instance_type" {
        description = "Type of EC2 instance"
        type        = string
        default     = "t2.micro"
      }


### Access and Pass Values to variables -


#### 1. Using a .tfvars File -
- Create a file_name.tfvars file.


      instance_type = "t3.medium"
      region        = "us-west-2"


terraform apply -var-file="terraform.tfvars"


#### 2. Using Command Line -

    terraform apply -var="instance_type=t3.medium"
    
#### 3. Using Environment Variables -

    export TF_VAR_instance_type="t3.medium"
    
- Terraform will automatically use this value.


## 2] Output Variables -
- An output variable in Terraform is used to display important values after running Terraform.
- It helps in getting information like public IPs, resource IDs, or other attributes of created resources.


      resource "aws_instance" "example" {
        ami           = "ami-12345678"
        instance_type = "t2.micro"
      }
      
      output "instance_public_ip" {
        description = "The public IP of the instance"
        value       = aws_instance.example.public_ip
      }


terraform apply

## 3] Local Variables -
- Local variables store reusable values inside Terraform.
- They help avoid repetition and make the code clean.

###### Without Local Variable (Repetition) -

          resource "aws_instance" "example1" {
            ami  = "ami-12345678"
            tags = {
              Environment = "Production"
              Owner       = "DevOps"
            }
          }
          
          resource "aws_instance" "example2" {
            ami  = "ami-12345678"
            tags = {
              Environment = "Production"
              Owner       = "DevOps"
            }
          }
         
         
         
##### Local Variable -
          
          locals {
            common_tags = {
              Environment = "Production"
              Owner       = "DevOps"
            }
          }
          
          resource "aws_instance" "example1" {
            ami  = "ami-12345678"
            tags = local.common_tags
          }
          
          resource "aws_instance" "example2" {
            ami  = "ami-12345678"
            tags = local.common_tags
          }
          


# Examples -

## variables.tf

          variable "region_name" {
          
            type    = string
          
            default = "ap-south-1"
          
          }
          
          variable "ins_type" {
             default = t2.micro
          
             type = string
          
          }
          
          variable "my_ami" {
          
             type = string
          
             default = "ami-00bb6a80f01f03502"
          
          }
          
          variable "vpc_id" {
          
             type = string
          
             default = "vpc-0ed0001bdda8ffe0d"
          
          }
          
          variable "my_access_key" {
          
            type = string
          
          }
          
          variable "secret_key" {
          
            type = string
          
          }



## tfvar file -


            region_name = "ap-south-1"
            ins_type    = "t2.micro"
            my_ami      = "ami-00bb6a80f01f03502"
            vpc_id      = "vpc-0ed0001bdda8ffe0d"
            my_access_key = "your-access-key-here"
            secret_key    = "your-secret-key-here"

 











