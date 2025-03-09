# User-data -

        provider "aws" {
          region = "us-east-1"  # Change region if needed
        }
        
        # Generate SSH key pair
        resource "tls_private_key" "rsa" {
          algorithm = "RSA"
          rsa_bits  = 4096
        }
        
        # Save the private key locally
        resource "local_file" "private_key" {
          content  = tls_private_key.rsa.private_key_pem
          filename = "mytf-key.pem"
        }
        
        # Create an AWS key pair using the public key
        resource "aws_key_pair" "my_key" {
          key_name   = "mytf-key"
          public_key = tls_private_key.rsa.public_key_openssh
        }
        
        # Create a Security Group for EC2
        resource "aws_security_group" "mysg" {
          name        = "web-server-sg"
          description = "Allow SSH and HTTP access"
        
          # Allow SSH access from anywhere (only for testing, restrict in production)
          ingress {
            from_port   = 22
            to_port     = 22
            protocol    = "tcp"
            cidr_blocks = ["0.0.0.0/0"]
          }
        
          # Allow HTTP access from anywhere
          ingress {
            from_port   = 80
            to_port     = 80
            protocol    = "tcp"
            cidr_blocks = ["0.0.0.0/0"]
          }
        
          # Allow all outbound traffic
          egress {
            from_port   = 0
            to_port     = 0
            protocol    = "-1"
            cidr_blocks = ["0.0.0.0/0"]
          }
        }
        
        # Create an EC2 instance with user_data
        resource "aws_instance" "myec2" {
          ami                    = "ami-0c02fb55956c7d316"  # Replace with a valid Amazon Linux AMI
          instance_type          = "t2.micro"
          key_name               = aws_key_pair.my_key.key_name
          vpc_security_group_ids = [aws_security_group.mysg.id]
        
          # User Data script to install Nginx
          user_data = <<-EOF
            #!/bin/bash
            sudo yum update -y
            sudo yum install nginx -y
            sudo systemctl start nginx
            sudo systemctl enable nginx
            echo "Hello from Terraform User Data!" | sudo tee /usr/share/nginx/html/index.html
          EOF
        
          tags = {
            Name = "MyTerraformEC2"
          }
        }








# Provisioners -
- Provisioners in Terraform are used to run scripts or commands after a resource is created.
- Provisioers are used to set up newly created resources, to execute scripts on a remote or local machine and to copy files to a remote machine.

# Types of Provisioners:
- Local-exec – Runs a command on your local machine.
- Remote-exec – Runs a command on the remote machine (like an EC2 instance).
- File – Copies files from your local machine to the remote machine.

## 1] Local-exec -
- Runs a command on your local machine (where Terraform is running).


        provider "aws" {
          region = "us-east-1"
        }
        resource "aws_instance" "example" {
          ami           = "ami-123456"  # Replace with a valid AMI
          instance_type = "t2.micro"
          key_name = "key_pair_name"
        
          provisioner "local-exec" {
            command = "echo 'EC2 Instance Created Successfully' > instance-info.txt"
          }
        }

## 2] Remote-exec – 
- Runs commands or scripts on other remote server over SSH.


        provisioner "remote-exec" {
            inline = [
              "sudo yum update -y",
              "sudo yum install nginx -y",
              "sudo service nginx start",
              "sudo sh -c 'echo Hello > /usr/share/nginx/html/index.html'"
            ]
          }
        
          connection {
            type        = "ssh"
            user        = "ec2-user"
            host        = self.public_ip
            private_key = tls_private_key.rsa.private_key_pem
          }

 



### Example -


      provider "aws" {
        region = "us-east-1"  # Change region if needed
      }
      
      # Create a Security Group for EC2
      resource "aws_security_group" "mysg" {
        name        = "web-server-sg"
        description = "Allow SSH and HTTP access"
      
        # Allow SSH access from anywhere (only for testing, restrict in production)
        ingress {
          from_port   = 22
          to_port     = 22
          protocol    = "tcp"
          cidr_blocks = ["0.0.0.0/0"]
        }
      
        # Allow HTTP access from anywhere
        ingress {
          from_port   = 80
          to_port     = 80
          protocol    = "tcp"
          cidr_blocks = ["0.0.0.0/0"]
        }
      
        # Allow all outbound traffic
        egress {
          from_port   = 0
          to_port     = 0
          protocol    = "-1"
          cidr_blocks = ["0.0.0.0/0"]
        }
      }
      
      # Create an EC2 instance
      resource "aws_instance" "myec2" {
        ami                    = "ami-0c02fb55956c7d316"  # Replace with a valid Amazon Linux AMI
        instance_type          = "t2.micro"
        key_name               = aws_key_pair.my_key.key_name
        vpc_security_group_ids = [aws_security_group.mysg.id]
      
        # Provisioner to install and start Nginx
        provisioner "remote-exec" {
          inline = [
            "sudo yum update -y",
            "sudo yum install nginx -y",
            "sudo systemctl start nginx",
            "sudo sh -c 'echo Hello from Terraform! > /usr/share/nginx/html/index.html'"
          ]
        }
      
        # SSH Connection Settings
        connection {
          type        = "ssh"
          user        = "ec2-user"
          host        = self.public_ip
          private_key = tls_private_key.rsa.private_key_pem
        }


## 3] File Provisioner -
- File provisioner is used to copy files or directories from the local machine to a remote machine.


      provisioner "file" {
        source      = "local_file.txt"
        destination = "/home/ubuntu/remote_file.txt"
      }


#### Example -


          provider "aws" {
            region = "us-east-1"  # Change as needed
          }
          
          # Generate SSH Key Pair using Terraform
          resource "tls_private_key" "rsa" {
            algorithm = "RSA"
            rsa_bits  = 4096
          }
          
          # Save the private key locally
          resource "local_file" "private_key" {
            content  = tls_private_key.rsa.private_key_pem
            filename = "my-key.pem"
          }
          
          # Create an AWS Key Pair using the generated public key
          resource "aws_key_pair" "my_key" {
            key_name   = "my-key"
            public_key = tls_private_key.rsa.public_key_openssh
          }
          
          # Create a Security Group for SSH and HTTP
          resource "aws_security_group" "mysg" {
            name        = "web-server-sg"
            description = "Allow SSH and HTTP access"
          
            ingress {
              from_port   = 22
              to_port     = 22
              protocol    = "tcp"
              cidr_blocks = ["0.0.0.0/0"]
            }
          
            ingress {
              from_port   = 80
              to_port     = 80
              protocol    = "tcp"
              cidr_blocks = ["0.0.0.0/0"]
            }
          
            egress {
              from_port   = 0
              to_port     = 0
              protocol    = "-1"
              cidr_blocks = ["0.0.0.0/0"]
            }
          }
          
          # Create an EC2 Instance
          resource "aws_instance" "example" {
            ami                    = "ami-0c55b159cbfafe1f0"  # Replace with a valid AMI
            instance_type          = "t2.micro"
            key_name               = aws_key_pair.my_key.key_name
            vpc_security_group_ids = [aws_security_group.mysg.id]
          
            # SSH Connection Settings for File Provisioner
            connection {
              type        = "ssh"
              user        = "ec2-user"  # Use "ubuntu" if it's an Ubuntu AMI
              private_key = tls_private_key.rsa.private_key_pem
              host        = self.public_ip
            }
          
            # File Provisioner to Copy a File
            provisioner "file" {
              source      = "local/path/to/localfile.txt"  # File in local system
              destination = "/home/ec2-user/remote_file.txt"  # File on EC2
            }
          
            tags = {
              Name = "TerraformInstance"
            }
          }
          
          

