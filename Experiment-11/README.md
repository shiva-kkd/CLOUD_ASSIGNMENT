# Experiment 11: Create Video Streaming Service Using S3 and CloudFront and AWS Elemental MediaConvert Digital Rights Management System

## Aim
To create a video streaming service using Amazon S3 and CloudFront.

## Prerequisites
- An active AWS account
- A test `.mp4` video file
- A web browser with internet access

## Procedure

### Step 1: Set up your Amazon S3 bucket
Storing raw video assets in a secure S3 bucket prevents unauthorized direct downloads while keeping them available for your CDN.

1. Log in to the AWS Management Console and go to **Services** > **S3**.
2. Click **Create bucket**.
   - Enter a globally unique name (e.g., `my-video-streaming-bucket-2026`).
   - Select your preferred AWS Region (e.g., `us-east-1` or the closest one).
3. Configure the settings:
   - **Block Public Access:** Keep **Block all public access** checked. The bucket must remain private to force users through CloudFront.
   - **Bucket Versioning:** Select **Enable**.
   - **Default Encryption:** Select **Enable** with **SSE-S3**.
4. Click **Create bucket** at the bottom.
5. **Upload a video:** Click on your new bucket name, select **Upload**, add a test `.mp4` video and click **Upload**.

### Step 2: Create a CloudFront distribution
CloudFront acts as the CDN. It retrieves your private S3 objects securely and distributes them to your users.

1. Search for and open the **CloudFront** console.
2. Click **Create distribution**.
3. **Origin settings:**
   - **Origin domain:** Select the S3 bucket you created in Step 1.
   - **Origin access:** Select **Origin access control settings (recommended)**.
   - **Origin access control (OAC):** Click **Create control setting**, leave the default settings and click **Create**. This securely connects CloudFront to your private S3 bucket.
4. **Default cache behavior settings:**
   - **Viewer protocol policy:** Select **Redirect HTTP to HTTPS**.
   - **Allowed HTTP methods:** Select **GET, HEAD**.
   - **Cache key and origin requests:** Choose **Cache policy and origin request policy (recommended)** and set the cache policy to **CachingOptimized**.
5. **Web Application Firewall (optional):** Select **Do not enable security protections** (for basic lab purposes).
6. Click **Create distribution** at the bottom of the page.

### Step 3: Update the S3 bucket policy for CloudFront
Because the S3 bucket is private, CloudFront needs permission to access the video files.

1. Once the distribution is created, a banner appears at the top prompting you to **Copy policy**. Copy the policy JSON provided.
2. Go back to the S3 console and click on your bucket.
3. Select the **Permissions** tab.
4. Scroll down to **Bucket policy** and click **Edit**.
5. Paste the copied CloudFront policy into the editor and click **Save changes**.

Example:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowCloudFrontServicePrincipal",
      "Effect": "Allow",
      "Principal": {
        "Service": "cloudfront.amazonaws.com"
      },
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::video-streaming-bucket/*"
    }
  ]
}
```

### Step 4: Test your streaming service
1. Go back to the CloudFront distributions page and wait for the status to change from **Deploying** to a **Last modified** date.
2. Copy the **Distribution domain name** (e.g., `d111111abcdef8.cloudfront.net`).
3. Open a new browser tab, paste the domain name and append the name of the uploaded video file to the end of the URL:
```
   https://d111111abcdef8.cloudfront.net/video.mp4
```
4. The video loads in the browser through the CloudFront stream.

## Output
The uploaded video plays in the browser through the CloudFront distribution domain name, while the S3 bucket remains private.

## Result
A video streaming service was successfully created using a private Amazon S3 bucket and Amazon CloudFront.

<img width="1600" height="900" alt="cloud111" src="https://github.com/user-attachments/assets/c6f785d1-7eac-4297-81e1-6595c2bc7d63" />

<img width="1600" height="900" alt="cloud112" src="https://github.com/user-attachments/assets/c2b8e82c-4f15-4726-af58-e022128ab8a2" />

