# Add AWS credentials in Terraform -
- There are four ways :


## 1]Environment Variables -
- Terraform automatically reads AWS credentials from environment variables.
- This is useful for local development and CI/CD pipelines.


    export AWS_ACCESS_KEY_ID="your-access-key"
    export AWS_SECRET_ACCESS_KEY="your-secret-key"
    export AWS_DEFAULT_REGION="us-east-1"  # (optional)


- You need to set these every time you open a new terminal session.

## 2] Configure AWS CLI -

    aws configure


- AWS will store these credentials in:
  - ~/.aws/credentials (for access keys)
  - ~/.aws/config (for region and profile settings)
 
  
## 3] Hardcoded in Terraform Code (Not Recommended) -

      provider "aws" {
        access_key = "your-access-key"
        secret_key = "your-secret-key"
      }


- Credentials are exposed in your Terraform code.
- If using Git, credentials can accidentally get pushed.


## 4] IAM Role (For EC2 Instances) -
- Attach an IAM role to your EC2 instance.
- Terraform will automatically use the role.






