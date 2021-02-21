# Sub40Fi.com

## Basics
This repo was generated following the tutorial at: [https://www.learnaws.org/2017/10/22/create-site-aws-using-s3/](https://www.learnaws.org/2017/10/22/create-site-aws-using-s3/)

### Running locally:
> jekyll serve

### AWS
#### Creating the initial S3 bucket
> aws s3 mb s3://sub40fi.com

Enable static website on that bucket
> aws s3 website s3://sub40fi.com/ --index-document index.html

create a file called `policy.json` and insert
```json
  {
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::sub40fi.com/*"
        }
    ]
  }
```

Add the policy to the bucket
> aws s3api put-bucket-policy --bucket sub40fi.com --policy file://policy.json

Sync the site
> aws s3 sync _site s3://sub40fi.com/ --delete


Go -
[http://sub40fi.com.s3-website-us-east-1.amazonaws.com/](http://sub40fi.com.s3-website-us-east-1.amazonaws.com)


