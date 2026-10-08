# Experiment 10: Deploy Static Web Application Using S3 on AWS and Secure It with Signed URLs

## Aim
To deploy a static web application using S3 on AWS and secure it with signed URLs.

## Prerequisites
- An active AWS account
- Website files (e.g., `index.html`, `styles.css`)
- A web browser with internet access

## Procedure

### Step 1: Create an AWS S3 bucket
1. On the AWS console, go to **S3** and click **Create bucket**.
2. Select the **AWS Region**.
3. Enter the **Bucket name**.
4. Uncheck **Block all public access**.
5. Leave the rest of the settings at default and click **Create bucket**.

### Step 2: Enable static website hosting
1. Open the bucket and select the **Properties** tab.
2. Scroll to the bottom, find **Static website hosting** and click **Edit**.
3. Enable static website hosting, set the index document (e.g., `index.html`) and click **Save changes**.

### Step 3: Add the bucket policy
1. Select the **Permissions** tab.
2. Under **Bucket policy**, click **Edit**.
3. Add the following policy (replace `BUCKET_NAME` with your bucket name) and click **Save changes**:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:*",
      "Resource": [
        "arn:aws:s3:::BUCKET_NAME/*",
        "arn:aws:s3:::BUCKET_NAME"
      ]
    }
  ]
}
```

### Step 4: Upload your files
1. Open your new bucket and click **Upload**.
2. Drag and drop your website files (e.g., `index.html`, `styles.css`) and click **Upload**.

The static application is now accessible on the S3 static website URL (found under **Properties** > **Static website hosting**).

### Step 5: Attach CloudFront with S3
CloudFront serves the static content from S3 with higher speed and lower latency.

1. From the AWS console, go to **CloudFront** and click **Create Distribution**.
2. Copy the static website URL from the S3 bucket properties and paste it into **Origin domain**. Remove `http://` / `https://` from the URL before pasting.
3. Select **Redirect HTTP to HTTPS** as the viewer protocol policy and set the **Allowed HTTP methods**.
4. Click **Create Distribution**.
5. Once the distribution is created, open your website using the **Distribution domain name**:

```
https://<distribution-domain-name>.cloudfront.net
```

## Output
- The website opens on the S3 static website URL.
- The website also opens through the CloudFront distribution domain name over HTTPS.

## Result
A static web application was successfully deployed using S3 on AWS and delivered through CloudFront.

<img width="961" height="400" alt="Screenshot 2026-10-07 235758" src="https://github.com/user-attachments/assets/309296a7-aaf2-48dd-b90d-bff8a57d503f" />
