---
title: "Free SSL Certificates powered by AWS ACM"
date: 2018-05-12T23:52:04+02:00
draft: false
---

In case you need SSL certificates for AWS services like CloudFront there is a very convenient 
way to obtain them. And best of all, it is free.

## Request a new certificate

Use the AWS CLI to request a new certificate. We are using DNS as validation method as this
is the best method to automate certificate renewal.

__Note:__ In case you plan to use the certificate for CloudFront make sure to create it in region 
`us-east-1` as this is mandatory for this service.

```
aws acm request-certificate \
  --domain-name sebastianvoss.com \
  --subject-alternative-names "*.sebastianvoss.com" \
  --idempotency-token "`date +%s`" \
  --region us-east-1 \
  --validation-method DNS
```

As a result the ARN of the certificate will be displayed. Now you can use the new
certificate in the other AWS services like CloudFront.

## Validate domain ownership

Before the certificate gets created you need to validate your domain ownership. Visit 
https://console.aws.amazon.com/acm/home?region=us-east-1/ to perform this task. As we
request DNS as validation method you need to add a special CNAME record. If your domain
is managed in Route 53 you just need to click on a button in the dashboard.

## Automatic renewal

AWS will automatically take care of certificate renewal before it expires. There is no
manual intervention required. You just need to make sure the special CNAME records are
present.
