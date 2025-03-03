# Providers -
- A provider in Terraform is a plugin that allows Terraform to interact with different cloud platforms (e.g., AWS, Azure, GCP).
- Terraform uses providers to manage and provision resources in the cloud or other services.
- Each Terraform configuration file must define the required provider.

        provider "aws" {
          region  = "us-east-1"
        }



| **Cloud Provider**  | **Terraform Provider**          | **Provider Source**                 |
|--------------------|--------------------------------|-------------------------------------|
| AWS              | `aws`                          | `hashicorp/aws`                    |
| Microsoft Azure  | `azurerm`                      | `hashicorp/azurerm`                |
| Google Cloud     | `google`                       | `hashicorp/google`                 |
| Oracle Cloud     | `oci`                          | `oracle/oci`                       |
| IBM Cloud       | `ibm`                          | `IBM-Cloud/ibm`                    |
| Alibaba Cloud   | `alicloud`                     | `aliyun/alicloud`                  |





