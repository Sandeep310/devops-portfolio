# devops-portfolio
# 🚀 CI/CD Pipeline for Static Website using AWS S3 & GitHub Actions

## 📖 Project Overview

This project demonstrates a complete **CI/CD (Continuous Integration & Continuous Deployment)** pipeline that automatically deploys a static website to AWS S3.

Whenever code is pushed to the `main` branch, a GitHub Actions workflow is triggered to upload the latest files to an S3 bucket and make them live instantly.

---

## 🌐 Live Demo

👉 http://my-devops-site-9119.s3-website.ap-south-2.amazonaws.com/

---

## 🏗️ Architecture

```
Developer → GitHub → GitHub Actions → AWS S3 → Public Website
```

---

## ⚙️ Tech Stack

* AWS S3 (Static Website Hosting)
* IAM (Identity and Access Management)
* GitHub Actions (CI/CD Automation)
* HTML

---

## 🔐 Security Implementation

* Used IAM User with programmatic access
* Stored AWS credentials securely using GitHub Secrets
* Avoided hardcoding sensitive information in the repository

> Note: For learning purposes, full S3 access was used. In production, least-privilege IAM policies should be applied.

---

## 📂 Project Structure

```
devops-portfolio/
│── index.html
│── README.md
│── .github/
│   └── workflows/
│       └── deploy.yml
```

---

## ⚡ CI/CD Workflow

1. Developer pushes code to GitHub repository
2. GitHub Actions workflow is triggered
3. AWS credentials are configured securely using secrets
4. Files are synced to S3 bucket using `aws s3 sync`
5. Website is updated automatically

---

## 🛠️ GitHub Actions Workflow

```yaml
name: Deploy Website to S3

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Code
        uses: actions/checkout@v4

      - name: Configure AWS Credentials
        uses: aws-actions/configure-aws-credentials@v4
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: ap-south-1

      - name: Deploy to S3
        run: |
          aws s3 sync . s3://your-bucket-name \
            --delete \
            --exclude ".git/*" \
            --exclude ".github/*"
```

---

## 🚀 How to Run This Project

### 1. Clone Repository

```
git clone https://github.com/your-username/devops-portfolio.git
cd devops-portfolio
```

### 2. Create S3 Bucket

* Enable static website hosting
* Set `index.html` as index document
* Configure public access and bucket policy

### 3. Setup IAM User

* Create IAM user with S3 access
* Generate Access Key & Secret Key

### 4. Add GitHub Secrets

* `AWS_ACCESS_KEY_ID`
* `AWS_SECRET_ACCESS_KEY`

### 5. Push Code

```
git add .
git commit -m "Initial setup"
git push origin main
```

---

## 🧠 Key Learnings

* Built an end-to-end CI/CD pipeline
* Understood AWS S3 static hosting
* Learned secure credential management using GitHub Secrets
* Gained hands-on experience with GitHub Actions automation

---

## 🔥 Future Improvements

* Add CloudFront (CDN + HTTPS)
* Implement least-privilege IAM policies
* Add linting step before deployment
* Add cache invalidation

---
## 👨‍💻 Author

Sandeep Gudimetla
