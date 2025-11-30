# Project: Implementing a Static Website Hosting Solution on Amazon S3

## Objective
Host a fully static website (HTML, CSS, JavaScript) on Amazon S3 with public access, eliminating the need for EC2 instances or web servers.

## Why This Solution is Cost-Effective, Scalable & Highly Available
- **Cost-Effective**: Pay-as-you-go pricing. Free tier includes 5 GB storage + 20,000 GET requests/month. No server maintenance costs.
- **Scalable**: S3 automatically scales to handle any amount of traffic — from 1 visitor to millions.
- **Highly Available**: 99.99% availability and 11 9s durability built-in. Multi-AZ by default.

## Workflow
1. Create S3 Bucket  
2. Upload Files  
3. Enable Static Website Hosting  
4. Add Bucket Policy  
5. Save → Access via Endpoint URL

## Prerequisites
- AWS Account
- Static website files (e.g., Tooplate Moso Interior template)

## Detailed Implementation Steps

### 1. Create S3 Bucket
- AWS Console → S3 → Create bucket
- Bucket name: Must be globally unique (e.g., `static-webpage-hosting-too-plate-2025`)
- Region: Choose your preferred region
- **Block all public access** → **Uncheck** (Must be disabled for public website)
- **Bucket Versioning** → **Enable** (Allows easy rollback to previous versions)
- Create bucket

### 2. Upload Files
- Download the Tooplate template ZIP file locally
- Extract it

**Local Terminal Commands (on your machine):**
```bash
wget "https://www.tooplate.com/zip-templates/2133_moso_interior.zip"
# Reason: Downloads the template directly from Tooplate

mv 2133_moso_interior.zip app.zip
# Reason: Renames for easier handling

unzip app.zip
# Reason: Extracts all HTML, CSS, JS, images
```

- In S3 Console → Open your bucket → Upload → Add folder → Upload all extracted files/folders
- After upload, if files are inside a subfolder:
  - Select all files/folders → Actions → Move
  - Destination: `s3://your-bucket-name/` (root of the bucket)
  - Move
> Reason: Static website hosting requires index.html at the bucket root

### 3. Enable Static Website Hosting
- Bucket → Properties tab → Static website hosting → Edit
- Select: **Enable**
- Index document: `index.html`
- (Optional) Error document: `error.html`
- Save changes

→ Copy the **Bucket website endpoint** (e.g., `http://static-webpage-hosting-too-plate.s3-website.us-east-1.amazonaws.com`)

### 4. Add Bucket Policy (Make Website Publicly Accessible)
- Bucket → Permissions → Bucket policy → Edit
- Paste this exact policy (replace `your-bucket-name`):

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::static-webpage-hosting-too-plate/*"
    }
  ]
}
```

- Save changes

> Explanation of Policy:
> - `"Principal": "*"` → Allows anyone (public access)
> - `"Action": "s3:GetObject"` → Permits reading files (required for website to load)
> - `"Resource": "arn:aws:s3:::bucket-name/*"` → Applies to all objects in the bucket

### 5. Verify Website
- Open the **Bucket website endpoint** in a browser
- Website loads successfully → Project Complete!

## Final Endpoint Example
```
http://static-webpage-hosting-too-plate.s3-website.us-east-1.amazonaws.com
```

## Optional Enhancements
- Add CloudFront → HTTPS + faster global delivery
- Use Route 53 → Custom domain (www.example.com)
- Enable S3 access logging

## Cleanup (Avoid Charges)
1. Disable Static website hosting
2. Remove bucket policy
3. Delete all objects
4. Delete bucket

