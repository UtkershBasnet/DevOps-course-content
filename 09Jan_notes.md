#### Date: 9th January 2026
# Introduction to Infrastructure Provisioning and Terraform

## 1. What is Infrastructure as Code (IaC)?
Infrastructure as Code (IaC) is the management and provisioning of 
infrastructure through code instead of through manual processes. 
- **Consistency:** Ensures the same environment is provisioned every time.
- **Speed:** Rapidly deploy infrastructure for development, testing, and 
  production.
- **Version Control:** IaC files can be versioned in Git just like application 
  code.
- **Scalability:** Easily duplicate infrastructure across different regions or 
  accounts.

## 2. Infrastructure Provisioning vs. Configuration Management
- **Provisioning:** Creating the infrastructure (Servers, Databases, Networks). 
  Tools: **Terraform**, CloudFormation.
- **Configuration Management:** Configuring software on existing infrastructure. 
  Tools: **Ansible**, Puppet, Chef.

## 3. What is Terraform?
Terraform is an open-source infrastructure as code software tool created by 
HashiCorp. It allows users to define and provide data center infrastructure 
using a high-level configuration language known as HashiCorp Configuration 
Language (HCL), or optionally JSON.

## 4. Key Terraform Concepts
- **Providers:** Plugins that Terraform uses to interact with cloud providers, 
  SaaS providers, and other APIs (e.g., `aws`, `google`, `azure`, `kubernetes`).
- **Resources:** The components of your infrastructure (e.g., a virtual 
  machine, a VPC, a DB instance).
- **Data Sources:** Allow data to be fetched or computed for use elsewhere in 
  Terraform configuration (e.g., fetching an existing AMI ID).
- **State File:** Terraform keeps track of the metadata of your infrastructure 
  in a `terraform.tfstate` file. This file is critical for Terraform to know 
  what it has created and what needs to be changed.
- **Variables and Outputs:** Allow for modular and reusable configurations.

## 5. The Terraform Workflow
1. **Write:** Define infrastructure in `.tf` files using HCL.
2. **Init:** Run `terraform init` to initialize the working directory and 
   download providers.
3. **Plan:** Run `terraform plan` to see what changes will be made without 
   actually applying them.
4. **Apply:** Run `terraform apply` to create or update the infrastructure.
5. **Destroy:** Run `terraform destroy` to tear down the infrastructure 
   managed by Terraform.

## 6. Declarative vs. Imperative IaC
Terraform is **Declarative**. You define the *desired state* (e.g., "I want 
3 servers"), and Terraform figures out how to make the actual state match the 
desired state.

## 7. Benefits of Terraform
- **Platform Agnostic:** Work with multiple cloud providers using the same 
  tool.
- **Resource Graph:** Terraform builds a graph of all resources to determine 
  dependencies and create resources in parallel.
- **Change Automation:** Complex changesets can be applied with minimal human 
  interaction.

## 8. Conclusion
Terraform is a cornerstone of modern DevOps. By treating infrastructure as 
code, teams can achieve a level of agility, reliability, and scale that was 
impossible with manual provisioning, paving the way for truly automated 
cloud-native environments.

---
*End of Notes*
