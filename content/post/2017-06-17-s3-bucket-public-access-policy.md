---
title: S3 bucket public access policy
date: '2017-06-17'
categories:
  - dev
  - S3
---

Use this policy for making a bucket public.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowPublicRead",
            "Effect": "Allow",
            "Principal": {
                "AWS": "*"
            },
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::mybucket/*"
        }
    ]
}
```




