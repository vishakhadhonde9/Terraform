# Create Security Group -


          provider "aws" {
            region = "us-east-1"  # Change to your desired AWS region
          }
          
          resource "aws_security_group" "my_sg" {
            name        = "my-security-group"
            description = "Allow SSH and HTTP"
          
            # Ingress Rule (Allow incoming traffic)
            ingress {
              from_port   = 22    # SSH
              to_port     = 22
              protocol    = "tcp"
              cidr_blocks = ["0.0.0.0/0"]  # Allows SSH from anywhere (use a more restricted IP for security)
            }
          
            ingress {
              from_port   = 80   # HTTP
              to_port     = 80
              protocol    = "tcp"
              cidr_blocks = ["0.0.0.0/0"]
            }
          
            # Egress Rule (Allow all outgoing traffic)
            egress {
              from_port   = 0
              to_port     = 0
              protocol    = "-1"
              cidr_blocks = ["0.0.0.0/0"]
            }
          
            tags = {
              Name = "MySecurityGroup"
            }
          }
          


# Create Instance from Security Group -


      resource "aws_instance" "my_instance" {
        ami           = "ami-0c55b159cbfafe1f0"  # Replace with a valid AMI ID for your region
        instance_type = "t2.micro"
      
        vpc_security_group_ids = [aws_security_group.my_sg.id]  # Attach the Security Group
      
        tags = {
          Name = "MyTerraformEC2"
        }
      }




# Create Keypair -


        provider "aws" {
          region = "us-east-1"  # Change to your desired AWS region
        }
        
        resource "aws_key_pair" "tf-key-pair" {
        
            key_name = "my-tf-key"
        
            public_key = tls_private_key.rsa.public_key_openssh
        
        }
        
        resource "tls_private_key" "rsa" {
        
            algorithm = "RSA"
        
            rsa_bits  = 4096
        
        }
        
        resource "local_file" "tf-key" {
        
           content  = tls_private_key.rsa.private_key_pem
        
           filename = "my-tf-key"
        
        }


      resource "aws_instance" "my_instance" {
        ami           = "ami-0c55b159cbfafe1f0"  # Replace with a valid AMI ID
        instance_type = "t2.micro"
        key_name      = aws_key_pair.tf-key-pair.key_name  # Attach the key pair
      
        tags = {
          Name = "MyTerraformEC2"
        }
      }




