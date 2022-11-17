---
title: "How to provision and deploy public SSL/TLS certicate using AWS Certificate Manager"
date: 2022-11-16T21:25:25-06:00
# weight: 1
# aliases: ["/first"]
tags: []
author: "Me"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: true
hidemeta: false
comments: true
description: ""
canonicalURL: "https://blog.darrelpol.com/posts/how-to-provision-and-deploy-public-certificates"
disableHLJS: true # to disable highlightjs
disableShare: true
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: true
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
editPost:
    URL: "https://github.com/poldarreldev/darrelpol.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---
Hello! Assuming that you've been following my "***How to start blogging using Amazon S3 and Amazon CloudFront***" blog series, you should already have a custom domain by now. If you haven't, checkout my blog about [How to get custom domain on Amazon Route 53](../how-to-get-custom-domain-on-amazon-route-53). 

On today's blog, I'm going to talk about how we can secure our custom domain by requesting an SSL/TLS certificate using AWS Certificate Manager or ACM.

Requesting a certificate using ACM is very easy. One thing to note tho, requesting for a public certificate is ***FREE,*** while requesting for a private certificate is not. On this tutorial, we're going to request for a public certificate for my `darrelpol.com` domain, and we're also going to include any future subdomain as part of the certificate. 

## Request a certificate
Like what I said, requesting is very easy. To start, log in to your AWS account and search for "**ACM**". And then, select and click "**Certificate Manager**" on the list.
![5-acm](/5-acm.png)


Next, click "**Request a certificate**".
![5-request-a-certificate](/5-request-a-certificate.png)

**NOTE:** You can import a Certificate on ACM, but we're not going to cover that here.

## Certificate type
For this tutorial, we want to request for a "*public certificate*". By default, public certificates are trusted by browsers and operating systems. Click "**Next**" once you're ready.
![5-request-a-certificate-2.png](/5-request-a-certificate-2.png)

## Request public certificate
On this step, we want to add additional names to our certificates. In my case, I wanted to also attach the names *www.darrelpol.com* and *\*.darrelpol.com*. By adding these names on the certificate, my readers will be able to reach my site by either names.
![5-request-public-certificate.png](/5-request-public-certificate.png)
For Validation methods, you can either choose email validation or DNS validation. Since I registered my domain on AWS Route 53, it's easier for me to get validated using DNS validation. If you did the same, I recommend using the recommended validation method.

![5-key-algorithm.png](/5-key-algorithm.png)
For Key algorithm, I'm not really sure yet what are the actual differences, but I suggest using the most widely used key type "**RSA 2048**" and only use other type if you really need to. 

Once you're ready, click "**Request**" and after a couple of minutes, you should see your certificate under the **"List Certificates"** tab.
![5-certificates.png](/5-certificates.png)


And just like that! You have now a certificate for your domain. On my next blog, I'm going to talk about the last and final blog for this series. I'm going to show you How to use Amazon CloudFront - a Low-Latency Content Delivery Network (CDN) to serve a static website hosted on Amazon S3. 

That's it for now. Thanks and see you on the next one! 

\- Darrel Pol