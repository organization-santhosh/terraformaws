# terraformaws
# Terraform AWS Project with GitHub Actions

This repository contains Terraform modules for deploying AWS resources using GitHub Actions for CI/CD. The repository is structured to support modular and reusable Terraform code.

## Repository Structure

```bash
modules/
  ├── ec2/
  ├── s3/
  └── vpc/
  Main.tf
  outputs.tf
  terraform.tfvars
  variables.tf

## Creating a GitHub Organization and Repository

### Step 1: Create a GitHub Organization

1. **Go to GitHub**:
   - Navigate to [GitHub](https://github.com/).

2. **Create a New Organization**:
   - Click on your profile picture in the top right corner.
   - Select `Your organizations`.
   - Click on `New organization`.
   - Choose a plan (free).
   - Fill in the necessary details and click `Create organization`.

### Step 2: Create a Repository in the Organization

1. **Navigate to Your Organization**:
   - Go to your organization's GitHub page.

2. **Create a New Repository**:
   - Click on the `New` button next to the repository tab.
   - Fill in the repository name (e.g., `terraformaws`).
   - Add a description if desired.
   - Choose the visibility (public or private).
   - Initialize the repository with a `README` file if desired.
   - Click `Create repository`.

## Pushing Code to GitHub

To push your code to GitHub, follow these steps:

1. **Clone the repository:**
   git clone https://github.com/your-organization/terraformaws.git
   cd terraformaws

2. **Add or update files in the repository as needed:**
   git add .
   git commit -m "Your commit message"

3. **Push to GitHub:**
   git push origin main

Configuring GitHub Actions
GitHub Actions are configured using YAML files placed in the .github/workflows directory. Before that create environment and add secrets.

1. **Add Environment Secrets:**
   Secrets, such as AWS credentials, should be stored securely in GitHub. To add secrets to your repository
   Navigate to Your GitHub Repository
   In your repository, click on the Settings tab located on the top menu
   In the left sidebar, click on Environments
   Click on New Environment
   Add Environment Name
   Click on Configure Environment
   Click on Add Environment Secret
   Add your both aws secret access key and access key id two times

2. Below is an example of a GitHub Actions workflow for deploying Terraform code, which we using in our project.
   https://github.com/organization-santhosh/terraformaws/blob/main/.github/workflows/workflow.yml
   ##Explanation:##
    Workflow Name and Trigger:
    The workflow is named "Terraform infra".
    It uses the workflow_dispatch event to allow manual triggering with an input parameter environment, which can be either dev or test.
    Job Definition:

    The job named terraform runs on an ubuntu-latest runner.
    The job's environment is set dynamically based on the input provided when the workflow is triggered.
    Permissions are set to allow read access to repository contents and write access to ID tokens.
    Defaults:

    Ensures that all run steps use the Bash shell.
    Steps:

    Checkout: Uses the actions/checkout@v3 action to clone the repository to the runner.
    Authenticate to AWS: Uses the aws-actions/configure-aws-credentials@v2 action to configure AWS credentials using secrets ACCESS_KEY and SECRET_KEY, and sets the AWS   region to ap-south-1.
    Setup Terraform: Uses the hashicorp/setup-terraform@v1 action to install Terraform.
    Terraform Init: Runs terraform init in the ./modules directory to initialize the Terraform configuration.
    Terraform Plan: Runs terraform plan -input=false in the ./modules directory to generate an execution plan.
    Terraform Apply: Runs terraform apply -auto-approve in the ./modules directory to apply the Terraform plan without interactive approval.
    This complete workflow file allows you to manually trigger a Terraform deployment with the specified environment, configure AWS credentials, and run the necessary   Terraform commands to manage your infrastructure.






