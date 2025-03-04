# Introduction -
- Terraform is an **Infrastructure as Code (IaC)** tool created by HashiCorp.
- . It allows you to define, provision, and manage infrastructure (like servers, databases, networks, and storage) using a declarative configuration language (HCL - HashiCorp Configuration Language).
- Terraform is a tool that helps you create and manage cloud resources using code instead of manually creating it.
- Terraform automates infrastructure deployment, reducing manual effort and human errors.

# Configuration -
## On Windows -
- Download Terraform:

      https://developer.hashicorp.com/terraform/downloads

- Select the Windows version and download the .zip file.

- Extract the .zip file.
- Move the terraform.exe file to folder that you created  program files.
- Add Terraform to System PATH:
    - Open Control Panel > System > Advanced System Settings > Environment Variables
    - Under "System Variables," select Path and click Edit
- Click New and add the Terraform directory path.
- Click OK and restart the terminal.
- Verify Installation:

      terraform version



# Terraform Lifecycle -

- Write Configuration:
  - Users define their infrastructure in a declarative configuration language, commonly using HashiCorp Configuration Language (HCL).
- Initialize:
  - Run terraform init to initialize a Terraform working directory. This step downloads the necessary providers and sets up the backend.
- Plan:
   - Run terraform plan to create an execution plan. Terraform compares the desired state from the configuration with the current state and generates a plan for the changes required to reach the desired state.
- Review Plan:
  - Examine the output of the plan to understand what changes Terraform intends to make to the infrastructure. This is an opportunity to verify the planned changes before applying them.
 
- Apply:
  - Execute terraform apply to apply the changes outlined in the plan. Terraform makes the necessary API calls to create, update, or delete resources to align the
infrastructure with the desired state.
 
- Destroy (Optional):
   - When infrastructure is no longer needed, or for testing purposes, run terraform
destroy to tear down all resources created by Terraform. This is irreversible, so use with caution.



