# Terraform Explanation

1. What is `terraform`?
   
    - Terraform alows you to automate and manage your infrastructure, your platform and your services run on that infrastructure. 
    - Terraform is a tool for `infrastructure provisioning`

        - It means before you deploy application you prepare infrastructure. There are some examples:
          - Create private network space
          - Create or change ec2 server instances 
          - install docker and other tools
          - create or add security configurations
          - create AWS users and permissions
        - `All of these, needs to be done in correct order, because one task maybe depends on them`
2. What are the differences between `Ansible` and `Terraform`?
    - Ansible is mainly a configuration tool:
       - it configures the infrastructure
       - deploy apps
       - install/update software or software provisioning
    - Terraform is mainly infrastructure provisioning tool
3. How does Terraform connect to the infrastructure platform provider?
   - For example how does terraform connect to AWS to create virtual space, start ec2 instaces, configure networks and etc

   `Terraform has two main components that make up it's architecture:`
    - `Core` > This uses two input sources to plan what needs to be created/updated/destroyed:
      - Terraform configuration or TF_Config
        - User write `What to create/configure`
      - Terraform State
        - Terraform keeps up-to-date state of how the current setup of the infrastructure lookslike
    - `Provider` > Such as AWS, Kubernetes and Fastly. 
      - Each provider gives terraform users access to it's resources
- There is an examle of how terraform configuration file looks like:
  ```
  # Configure the AWS Provider
  provider "aws" {
    version = "~> 2.0"
    region = "us-east-1"
  }

  # Create a VPC
  resource = "aws_vpc" "example" {
    cidr_block = "10.0.0.0/16"
  }
  ``` 
- `Terraform is a Declarative tool`
  - It means instead of defining what steps to be executed to create the vpc or two spin up five ec2 instances, `you define the end state you desire in your config file and terraform figures out what needs to be done`:
    - For example: 
      - I want 5 servers with following network config
      - AWS user with following permission
4. How do you make terraform take action?
   - Terraform has commands and you can execute to go through different stages:
     1. Refresh: With this command, terraform will query infrastructure provider to get current state. Terraform will now know what is the current state of the infrastructure
     2. Plan: This commad indicate that what terraform needs to do in order to achieve the desired state that you defined in terraform configuration file. `This is just a preview, no changes to real resources`
     3. Apply: With this command you can execute the plan
     4. Destroy: This will destroy the whole setup, removing elements one by one in a right order and cleaning up all the resources
