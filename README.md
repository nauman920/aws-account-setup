# How to Create an AWS Free Tier Account

### Introduction

Amazon Web Services (AWS) provides a Free Tier account that allows users to explore cloud computing without upfront costs. In this guide, you’ll learn how to sign up for an AWS Free Tier account and get started with cloud services.

### Step 1: Visit the AWS Free Tier Page

Go to [AWS Free Tier](https://aws.amazon.com/free/) to review the services available. 
Click the “Create a Free Account” button.

### Step 2: Sign Up with Your Email
Enter your email address, choose a username, and set a strong password. Click “Continue” to proceed.

### Step 3: Provide Personal and Payment Information
Fill in your personal details, including your name and phone number. AWS requires a credit or debit card for identity verification, but you won’t be charged for Free Tier usage.

### Step 4: Verify Your Identity
AWS will send a verification code via text or voice call. Enter the code to verify your identity.


### Step 5: Choose a Support Plan
Select the Basic Support plan, which is free. You can upgrade later if needed.


### Step 6: Sign In to AWS Console
Once your account is set up, log in to the AWS Management Console to start exploring services like EC2, S3, and Lambda.


## Conclusion
Creating an AWS Free Tier account is a simple process that opens the door to cloud computing. Start experimenting with AWS services today!

Thank you taking the time to read my article! Let’s connect!






1. [Install Terraform](https://learn.hashicorp.com/terraform/getting-started/install.html)
2. Create AWS account
3. If the file `~/.aws/credentials` does't exist, create it and add you Terraform profile to the file. For example:
   ```text
   [terraform]
   aws_access_key_id = Your access key
   aws_secret_access_key = Your secret access key 
   ```
4. Create S3 bucket to store Terraform state
5. Create config file `./src/free-tier/backend/config.tf` that will contain information how to store state in a given bucket. See [example](./src/free-tier/backend/example.config.tf).
6. Create SSH key pair to connect to EC2 instance:
   ```bash
   cd ./src/free-tier/provision/access

   # it creates "free-tier-ec2-key" private key and "free-tier-ec2-key.pub" public key
   ssh-keygen -f free-tier-ec2-key
   ``` 
   
### Build infrastructure

1. `cd ./src/free-tier`
2. `terraform init -backend-config="./backend/config.tf"`
3. `terraform plan`
4. `terraform apply`

### Post steps

After building the infrastructure you can try to connect to you `EC2 instance` via SSH:

1. `cd ./src/free-tier`
2. `ssh -i ./provision/access/free-tier-ec2-key ubuntu@[EC2 public IP]`

To check HTTP access you can install `apache2` on your EC2 instance:

1. `sudo apt update && sudo apt install apache2` (on EC2 machine)
2. `sudo service apache2 start` (on EC2 machine) 
3. Check in browser: `http://[EC2 public IP]/`. You can see `Apache2 Default Page` (something like [this](https://annex.exploratorium.edu/))

To destroy infrastructure:

1. `cd ./src/free-tier`
2. `terraform destroy`

### Similar projects

* https://github.com/rogeriomm/aws-lab
