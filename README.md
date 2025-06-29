# aws-codepipeline-github-action-s3
 Deploy portfolio  with Full CI/CD Pipeline on AWS | GitHub + CodePipeline + S3 

#✅ Overview
You’ll:

Host your portfolio website on S3 (static site).

Use CodePipeline to automatically deploy whenever you push to GitHub.

Use CodeBuild to fetch and build the source.

Use GitHub as the source provider.

🚀 Step-by-Step Implementation

Step 1: 🧾 Create an S3 Bucket
Go to S3 > Create Bucket

Name it: my-portfolio-bucket (must be globally unique)

Uncheck Block all public access

Enable static website hosting

Index document: index.html

Save and note the S3 website URL

Step 2: ⚙️ Set S3 Bucket Policy
Go to Permissions > Bucket Policy and paste:
Replace my-portfolio-bucket with your actual bucket name.

Step 3: 💻 Push Code to GitHub

Step 4: 🔧 Create a BuildSpec File
In your project root, create a buildspec.yml:

Step 5: 🛠️ Create CodeBuild Project
Go to AWS CodeBuild > Create project

Name: PortfolioBuild

Source provider: GitHub (connect via OAuth)

Environment:

Managed image: Amazon Linux 2

Runtime: Standard

Buildspec: Use buildspec.yml from source

Artifacts:

Type: Amazon S3

Bucket: my-portfolio-bucket

Name: / (root)

Step 6: 🔁 Create CodePipeline
Go to AWS CodePipeline > Create pipeline

Name: PortfolioPipeline

Source:

Provider: GitHub

Repository: Select your portfolio repo

Build:

Provider: AWS CodeBuild

Project: PortfolioBuild

Deploy:

Skip deploy stage (S3 upload is already handled in CodeBuild)

Step 7: 🌐 Access Your Portfolio
Visit your S3 Static website URL, like:
http://my-portfolio-bucket.s3-website-us-east-1.amazonaws.com
🌀 CI/CD Flow Diagram

GitHub Repo (main branch)
         ↓ (push)
AWS CodePipeline
         ↓
   AWS CodeBuild (uses buildspec.yml)
         ↓
     Deploy to S3 Bucket (Static Website Hosting)
         ↓
      Live Portfolio Website

#✅ FOR References 1. https://www.youtube.com/watch?v=1k6s4shjpRc
               2.https://github.com/CSEngineer1412/aws-codepipeline-react-s3?tab=readme-ov-file
