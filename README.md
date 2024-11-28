# Static Website Hosting on AWS with CI/CD 🚀

This project demonstrates hosting a static website on AWS using **Amazon S3** for storage, **CloudFront** for content delivery, and **Route 53** for DNS management. Additionally, a **CI/CD pipeline** has been implemented to automate updates to the website whenever changes are pushed to the GitHub repository.

---

## Table of Contents
- [Introduction](#introduction)
- [Architecture Diagram](#architecture-diagram)
- [Features](#features)
- [Technologies Used](#technologies-used)
- [Setup and Deployment](#setup-and-deployment)
  - [Step 1: Create an S3 Bucket](#step-1-create-an-s3-bucket)
  - [Step 2: Set Up CloudFront](#step-2-set-up-cloudfront)
  - [Step 3: Configure Route 53](#step-3-configure-route-53)
  - [Step 4: Implement CI/CD with GitHub Actions](#step-4-implement-cicd-with-github-actions)
- [Challenges Faced](#challenges-faced)
- [Key Takeaways](#key-takeaways)
- [Resources](#resources)

---

## Introduction
This project aims to provide a hands-on understanding of:
- Hosting static websites on AWS.
- Configuring and using AWS services such as **S3**, **CloudFront**, and **Route 53**.
- Automating deployment using **CI/CD pipelines** with **GitHub Actions**.

---

## Architecture Diagram
Below is the architecture of the setup:

1. **S3 Bucket**: Stores the static website files (HTML, CSS, JS).
2. **CloudFront**: Distributes content globally with low latency.
3. **Route 53**: Manages DNS for custom domain routing.
4. **GitHub Actions**: Automates the deployment process.

*Include your architecture diagram here (e.g., from Lucidchart or draw.io).*

---

## Features
- **Secure and Scalable Hosting**: Leveraging AWS S3 and CloudFront for secure and scalable delivery.
- **CI/CD Pipeline**: Automatically deploys updated website content on every push to the GitHub repository.
- **Custom Domain Integration**: Route 53 ensures seamless integration with a custom domain.
- **Global Availability**: CloudFront ensures high availability and low latency across the globe.

---

## Technologies Used
- **AWS S3**: For static file storage and website hosting.
- **CloudFront**: For content delivery and caching.
- **Route 53**: For DNS management.
- **GitHub Actions**: For CI/CD pipeline.
- **draw.io/Lucidchart**: For architecture visualization.

---

## Setup and Deployment

### Step 1: Create an S3 Bucket
1. Log in to your AWS account.
2. Navigate to **S3** and create a new bucket.
3. Enable static website hosting and upload your static files.
4. Make the bucket publicly accessible (only for demonstration purposes).

### Step 2: Set Up CloudFront
1. Go to **CloudFront** and create a new distribution.
2. Use your S3 bucket as the origin.
3. Configure caching and HTTPS settings.
4. Note the CloudFront URL for later use.

### Step 3: Configure Route 53
1. Purchase or use an existing domain in Route 53.
2. Create an A or CNAME record to point to the CloudFront distribution.
3. Verify the domain works as expected.

### Step 4: Implement CI/CD with GitHub Actions
1. Add a `.github/workflows/deploy.yml` file to your repository with the following content:

```yaml
name: Deploy to S3

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Configure AWS Credentials
        uses: aws-actions/configure-aws-credentials@v2
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: us-east-1

      - name: Sync Files to S3
        run: |
          aws s3 sync ./static s3://your-bucket-name --delete
```
2. Add your AWS Access Key and Secret Key as GitHub Secrets.

---

## Challenges Faced

- S3 permissions: Emsuring files are publicily accessible without compromising security.
- Domain Propogation Dellays: Waiting for DNS changes to propagate globally.
- CI/CD Debugging: Troubleshooting deployment failures in GitHub Actions
  
---

## Key Takeaways

- Setting up a static website hosting environment involves multiple AWS services working together.
- CI/CD pipelines significantly improve development workflow efficiency.
- DNS and content delivery configuration is critical for performance and user experience.


