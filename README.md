# GitHub Actions Workflow: Create Terraform Cloud Project

This GitHub Actions workflow automates the creation of a project in Terraform Cloud. It ensures that a project is not recreated if it already exists, making it efficient and reliable for managing Terraform Cloud projects.

## Features

- **Project Existence Check**: Skips project creation if the specified project already exists in Terraform Cloud.
- **Manual Trigger**: Can be manually triggered via GitHub Actions with customizable inputs.
- **Secure Authentication**: Uses a Terraform Cloud API token stored as a GitHub Secret.

## Prerequisites

1. **Terraform Cloud API Token**:
   - Generate a Personal Access Token (PAT) in [Terraform Cloud](https://app.terraform.io/).
   - Add the token to your GitHub repository as a secret:
     - Navigate to `Settings > Secrets and variables > Actions`.
     - Create a new secret named `TFC_API_TOKEN` and paste the PAT.

2. **Organization Name**:
   - Update the `TFC_ORG` variable in the workflow YAML file to your Terraform Cloud organization name.

## Workflow Inputs

| Input Name           | Description                                   | Required | Default Value               |
|----------------------|-----------------------------------------------|----------|-----------------------------|
| `project_name`       | Name of the Terraform Cloud project to create| Yes      | `new_project`              |
| `project_description`| Description of the Terraform Cloud project   | No       | `A new Terraform Cloud project created via GitHub Actions` |
| `org_name`           | Name of the Terraform Cloud Org              | Yes      | `CloudMania` |

## Workflow Steps

1. **Check for Project Existence**:
   - Queries Terraform Cloud to see if the specified project already exists.
   - If it exists, skips the project creation step.

2. **Create Project**:
   - If the project does not exist, it sends a `POST` request to Terraform Cloud to create the project.

3. **Confirm Project Creation**:
   - Verifies the existence of the project (whether pre-existing or newly created).
