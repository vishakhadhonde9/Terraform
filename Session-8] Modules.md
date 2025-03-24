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

