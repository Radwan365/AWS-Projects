This repository contains the source code and deployment pipeline for my portfolio website, hosted as a static website on AWS S3. The project demonstrates my skills in web development, JavaScript, cloud infrastructure setup, and implementing CI/CD pipelines.

Features

Static Website Hosting: Fully responsive single-page website hosted on an AWS S3 bucket.

Interactive Elements: JavaScript used for dynamic behavior such as form validation, interactive menus, and smooth scrolling.

CI/CD Pipeline: Continuous integration and deployment pipeline implemented to automate updates and deployment.

Cloud Infrastructure: Leveraged AWS services such as S3, CloudFront, and Route 53 for hosting and DNS management.

Development Workflow: Developed and tested locally using Visual Studio Code (VS Code).

Tech Stack:

Frontend: HTML, CSS, JavaScript

CI/CD: GitHub Actions, AWS CLI

Hosting: AWS S3


Project Workflow
1. Website Creation
The website consists of the following sections:

Home: A welcoming landing page with smooth scrolling and animations.

About: Highlights my professional background, skills, and interests.

Skills: Technical expertise and certifications.

Projects: A showcase of my key projects.

Contact: Interactive form for inquiries and links to my social profiles.

JavaScript functionality includes:

Form validation in the Contact section.

Smooth scrolling for navigation links.

Dynamic updates to the Skills and Projects sections.

Editor: Developed locally using Visual Studio Code.

Extensions:

Live Server: Used for real-time previews of the website during development.

GitLens: Facilitates Git integration and version control directly in VS Code.

GitHub Integration: VS Code is linked to GitHub for easy version control and pushing changes to the repository.

2. AWS S3 Static Website Hosting
   
Configured an S3 bucket for static website hosting.

Enabled public access and configured bucket policy for website accessibility.

Files were automatically deployed via GitHub Actions.

4. CI/CD Pipeline
   
GitHub Actions Workflow:

Triggered on every push to the main branch.

Automatically deploys updated files to the S3 bucket.

Workflow overview:

Code changes are made in VS Code.

Configure AWS credentials securely using GitHub Secrets.

Sync the repository files to the S3 bucket using aws s3 sync.

Prerequisites

1. AWS Account

- S3 bucket configured for static website hosting.
- IAM user with the necessary permissions.
  
2. VS Code Setup

- Install extensions such as Live Server, Prettier, and GitLens.
  
-Link VS Code to your GitHub repository for seamless version control.

3. GitHub Repository

- Set up GitHub Secrets for AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY to securely connect to AWS.

Deployment

Manual Deployment

- Use VS Code to edit and preview your files locally.
- Upload files to the S3 bucket using AWS CLI:
  aws s3 sync . s3://radwan-tech-bucket --delete  

Automated Deployment with GitHub Actions

1. Create a .github/workflows/deploy.yml file in your repository:

name: Upload Website

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v2

      - name: Install AWS CLI
        run: |
          sudo apt-get update
          sudo apt-get install -y awscli

      - name: Configure AWS
        uses: aws-actions/configure-aws-credentials@v1
        with:
          aws-region: eu-west-2
          AWS-ACCESS-KEY-ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS-SECRET-ACCESS-KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}

      - name: Deploy web app
        run: aws s3 sync ./Client s3://radwan-tech-bucket --delete
        
 2. Push changes to trigger the deployment workflow.

Required IAM Permissions

The IAM user must have the following permissions:

{
    "Version": "2012-10-17",
    "Id": "Policy1730381383814",
    "Statement": [
        {
            "Sid": "Stmt1730381374183",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::209479306146:user/Radwan"
            },
            "Action": "s3:*",
            "Resource": [
                "arn:aws:s3:::radwan-tech-bucket",
                "arn:aws:s3:::radwan-tech-bucket/*"
            ]
        }
    ]
}

Tools & Technologies

- Visual Studio Code: Local development and testing.

- Frontend: HTML, CSS, JavaScript.

- AWS: S3 for hosting, IAM for security, AWS CLI for deployment automation.

- GitHub Actions: Automates deployment to AWS S3.
