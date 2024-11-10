Swiggy-Clone DevOps Project Setup Guide
This guide walks through setting up a CI/CD pipeline for the Swiggy-Clone application, integrating Terraform, AWS CLI, Jenkins, Docker, and SonarQube. Follow these instructions to configure each component properly.

1. AWS CLI Configuration
To connect to AWS using the CLI, first configure the AWS CLI with your IAM user credentials.

IAM User Details:

IAM User Name: 
Access Key: 
Secret Access Key: 
Terminal Commands:

bash
Copy code
aws configure
During Configuration, Input:

Region Name: (Specify the AWS region you will be using, e.g., us-west-2).
After configuration, verify the setup using AWS CLI commands like aws s3 ls.

2. Terraform Commands
Initialize, plan, and apply Terraform scripts to provision infrastructure on AWS.

Commands:

bash
Copy code
terraform init          # Initialize Terraform configuration
terraform plan          # Generate and show execution plan
terraform apply --auto-approve  # Apply the changes to reach the desired state
3. System Update and Jenkins Setup
Commands:

bash
Copy code
sudo apt update                    # Update package list
java --version                     # Check Java version (ensure Java is installed for Jenkins)
sudo systemctl status jenkins      # Check Jenkins status
Jenkins Access:

Copy the public IP and add :8080 to access Jenkins.
Retrieve Jenkins Initial Password:

bash
Copy code
cat /var/lib/jenkins/secrets/initialAdminPassword
SonarQube Access:

Copy the public IP and add :9000 to access SonarQube.
Default SonarQube Login: admin/admin
4. Jenkins Plugin Setup
In Jenkins, install the required plugins for the Swiggy-Clone pipeline.

Go to Manage Jenkins > Manage Plugins.
Install the following plugins:
Eclipse
Pipeline Stage View
SonarQube Scanner
NodeJS
OWASP Dependency-Check
Docker
Docker Commons
Docker Pipeline
Docker API
Docker Build Step
5. Configure Tools in Jenkins
Configure Jenkins tools for this project.

Navigate to Manage Jenkins > Global Tool Configuration.
Add the following tools:
JDK: Name jdk17, set to auto-install from adoptium.net with version jdk-17.0.11.+9.
Git: Install Git for version control.
SonarQube Scanner: Name sonar-scanner.
NodeJS: Name node23, version nodejs23.0.0.
Docker: Name docker, version latest.
OWASP Dependency-Check: Name DP-Check, version 10.0.4.
6. SonarQube Configuration
Create a SonarQube Token
Go to Administration > Security > Users.
Generate a token named token.
Configure SonarQube in Jenkins
Go to Manage Jenkins > Manage Credentials > Global > Add Credentials.
Select Kind: Secret Text.
Secret Text: Paste the SonarQube token generated.
Set ID as Sonar-token.
SonarQube Webhook Setup
In SonarQube, go to Administration > Webhooks.
Create a webhook with:
Name: jenkins
URL: http://<jenkins-ip>:8080/sonarqube-webhook/
Configure SonarQube Server in Jenkins
Go to Manage Jenkins > Configure System > SonarQube Servers.
Add SonarQube Server details:
Name: sonar-server
URL: http://<sonarqube-ip>:9000
Credentials: Select Sonar-token.
7. Docker Hub Credentials
To connect Jenkins to Docker Hub:

Go to Manage Jenkins > Manage Credentials > System > Global credentials.
Add Kind: Username with password.
Username: (Your Docker Hub username)
Password: (Your Docker Hub password)
ID: docker
8. Create Jenkins Job for Swiggy Application
In Jenkins, click on New Item.
Name the item Swiggy-application.
Select Pipeline as the project type and configure your pipeline script as necessary.
9. Docker Commands for Verification
Use the following Docker commands to verify images and running containers:

bash
Copy code
docker images        # List all Docker images
docker ps            # List all running Docker containers
This completes the setup guide for your Swiggy-Clone DevOps project. Each step provides a configuration or installation essential for setting up a CI/CD pipeline with Jenkins, SonarQube, Docker, and Terraform.
