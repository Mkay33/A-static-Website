# A-static-Website
Hosting a Static Website on AWS S3 + CloudFront

This guide explains how to deploy a fast, secure, and scalable static website using Amazon S3 for storage and Amazon CloudFront as a global CDN.

📌 Overview

You will learn how to:

Create and configure an S3 bucket for static website hosting

Upload your website files (index.html, style.css, images, etc.)

Configure public access, Bucket Policy, and Static Hosting

Create a CloudFront Distribution

(Optional) Add a custom domain + HTTPS certificate

Deploy updates to your website

🛠 Prerequisites

Before you begin, ensure you have:

An AWS account

Basic knowledge of HTML/CSS/JS

Website files ready to upload

(Optional) A domain name in Route 53 (or another registrar)

1. Create and Configure an S3 Bucket
1.1 Create a Bucket

Go to S3 Console

Click Create bucket

Enter a unique bucket name
Example: my-static-website-demo

Choose your region

Uncheck "Block all public access"

Confirm enabling public access

Click create bucket
<img width="1891" height="861" alt="image" src="https://github.com/user-attachments/assets/f1d30154-f4d7-4e57-86b3-7a27fcf520b2" />

<img width="1872" height="791" alt="image" src="https://github.com/user-attachments/assets/cea83114-7c73-4d14-8f2c-09801132656d" />


1.2 Enable Static Website Hosting

Open your bucket

Go to Properties

Scroll to Static website hosting

Enable it

Set:
<img width="1887" height="747" alt="image" src="https://github.com/user-attachments/assets/885f2f94-6d42-4677-baa9-796695e60f83" />

Index document → index.html

Error document → error.html (optional)

<img width="1891" height="816" alt="image" src="https://github.com/user-attachments/assets/9fdfbb38-2615-4417-8475-db2732d9332f" />
Save changes

You’ll get a Static Website URL, like:

http://my-static-website-demo.s3-website-us-east-1.amazonaws.com

1.3 Set Bucket Policy (Make Files Public)

Go to Permissions → Bucket Policy, paste:

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::my-static-website-demo/*"
    }
  ]
}


Replace my-static-website-demo with your own bucket name.
<img width="1888" height="899" alt="image" src="https://github.com/user-attachments/assets/11f17b9f-8437-46b8-bfd4-ed338df67b7a" />

Save.

1.4 Upload Website Files

Go to Objects

Click Upload

Upload:

index.html
style.css
script.js
images/

<img width="1897" height="836" alt="image" src="https://github.com/user-attachments/assets/2c2f5944-899a-4a24-a523-d9f4ff11f157" />

Click Upload

Your website is now accessible via the S3 website endpoint.

2. Create a CloudFront Distribution
<img width="1946" height="828" alt="image" src="https://github.com/user-attachments/assets/2653f684-db46-4762-b6aa-3a963175298e" />

CloudFront gives you:

✓ HTTPS
✓ Global caching
✓ Faster load times
✓ Security

2.1 Create Distribution

Go to CloudFront Console

Click Create Distribution
<img width="1946" height="828" alt="image" src="https://github.com/user-attachments/assets/eae4d9ae-229f-42f8-9191-33d12afded94" />

Under Origin:
<img width="1885" height="827" alt="image" src="https://github.com/user-attachments/assets/9c116bbf-7715-4ddd-a1dd-5a61940af8ba" />

Origin domain → select your S3 bucket (the one ending with .amazonaws.com)

Do NOT use the S3 website endpoint here
<img width="1895" height="768" alt="image" src="https://github.com/user-attachments/assets/a76663f4-1e21-4346-9388-41071c740e01" />
<img width="1912" height="833" alt="image" src="https://github.com/user-attachments/assets/34132c3f-8388-45d2-907d-bd16296d5b1c" />

Settings:
<img width="1890" height="836" alt="image" src="https://github.com/user-attachments/assets/69ab55a4-ff63-4f4d-a356-ba928e25e2df" />

Viewer protocol policy: Redirect HTTP to HTTPS

Cache policy: CachingOptimized

Compress objects automatically: Yes

Click Create Distribution

Wait 5–10 minutes.

2.2 Get Your CloudFront URL

After deployment, you’ll get:

https://d123abcd1234.cloudfront.net


This is now your new website URL!
<img width="1183" height="372" alt="image" src="https://github.com/user-attachments/assets/0fbe523c-f4af-49f5-8ca4-3357c076fe2a" />

