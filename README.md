# Project-9: Implementing a Static Website Hosting Solution on Amazon S3

## Implementing a Cost-Effective Static Website Hosting Solution on Amazon S3

In this project, we implement a highly cost-effective and scalable solution for hosting static websites using Amazon Simple Storage Service (S3). The goal is to demonstrate how S3 can be used to host static web content, such as HTML, CSS, JavaScript files, while leveraging S3's inherent benefits, such as high availability, durability, and cost optimization.

## Bucker Creation

AWS → S3 → Create Bucket

static-webpage-hosting-too-plate

Block Public Access settings for this bucket

Unselect the Block all public access 

Bucket Versioning : Enable

[ Create bucket ]

S3 → static-webpage-hosting-too-plate

## Upload

Download the previously we copied link website url. This files download to our computer

wget <Link of the download button>

ls

mv 2133_moso_interior app.zip

open .

unzip app.zip

Add Folder

Upload the folder

[ Upload ]

All the folders move to root folder of the bucket

Select all folders → Actions → Move 

Destination : s3://static-webpage-hosting-too-plate/

[ Move ]

## Enabling static website hosting

Amazon S3 → Buckets → static-webpage-hosting-too-plate → Properties → Static website hosting → Edit

Enable

Index Document : index.html

[ Save changes ]

Bucket website endpoint

Copy the link and paste on a browser

## Bucket policy and verify

Amazon S3 → Buckets → static-webpage-hosting-too-plate → Permissions → Bucket policy → Edit

{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::<Your Bucket Name>/*"
        }
    ]
}

Add this code to the policy section

[ Save Changes ]

Then refresh the website there loaded.

Finished …….!!!!!!!!!
