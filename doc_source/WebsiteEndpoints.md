# Website Endpoints<a name="WebsiteEndpoints"></a>

When you configure your bucket as a static website, the website is available at the AWS Region\-specific website endpoint of the bucket\. Website endpoints are different from the endpoints where you send REST API requests\. For more information about the differences between the endpoints, see [Key Differences Between a Website Endpoint and a REST API Endpoint](#WebsiteRestEndpointDiff)\.

Depending on your Region, Amazon S3 website endpoints follow one of these two formats\. The URL returns the default index document that you configure for the website:

```
http://bucket-name.s3-website.Region.amazonaws.com
```

```
http://bucket-name.s3-website-Region.amazonaws.com
```

For a complete list of Amazon S3 website endpoints, see [Amazon S3 Website Endpoints](https://docs.aws.amazon.com/general/latest/gr/s3.html#s3_website_region_endpoints) in the *AWS General Reference*\.

For your customers to access content at the website endpoint, you must make all your content publicly readable\. To do so, you can edit the S3 Block Public Access settings for the bucket\. For more information, see [Using Amazon S3 Block Public Access](access-control-block-public-access.md)\. Then, use a bucket policy or an access control list \(ACL\) on an object to grant the necessary permissions\. For more information, see [Permissions Required for Website Access](WebsiteAccessPermissionsReqd.md)\.

**Important**  
Amazon S3 website endpoints do not support HTTPS\. For information about using HTTPS with an Amazon S3 bucket, see the following:  
[How do I use CloudFront to serve HTTPS requests for my Amazon S3 bucket?](https://aws.amazon.com/premiumsupport/knowledge-center/cloudfront-https-requests-s3)
[Requiring HTTPS for Communication Between CloudFront and Your Amazon S3 Origin](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/using-https-cloudfront-to-s3-origin.html)
Requester Pays buckets  do not allow access through the website endpoint\. Any request to such a bucket receives a 403 Access Denied response\. For more information, see [Requester Pays Buckets](RequesterPaysBuckets.md)\.

**Topics**
+ [Website Endpoint Examples](#website-endpoint-examples)
+ [Adding a DNS CNAME](#website-endpoint-dns-cname)
+ [Using a Custom Domain with Route 53](#custom-domain-s3-endpoint)
+ [Key Differences Between a Website Endpoint and a REST API Endpoint](#WebsiteRestEndpointDiff)

## Website Endpoint Examples<a name="website-endpoint-examples"></a>

The following examples show how you can access an Amazon S3 bucket that is configured as a static website\.

**Example — Requesting an Object at the Root Level**  
To request a specific object that is stored at the root level in the bucket, use the following URL structure\.  

```
http://bucket-name.s3-website.Region.amazonaws.com/object-name
```
For example, the following URL requests the `photo.jpg` object that is stored at the root level in the bucket\.  

```
http://example-bucket.s3-website.us-west-2.amazonaws.com/photo.jpg
```

**Example — Requesting an Object in a Prefix**  
To request an object that is stored in a folder in your bucket, use this URL structure\.  

```
http://bucket-name.s3-website.Region.amazonaws.com/folder-name/object-name
```
The following URL requests the `docs/doc1.html` object in your bucket\.   

```
http://example-bucket.s3-website.us-west-2.amazonaws.com/docs/doc1.html
```

## Adding a DNS CNAME<a name="website-endpoint-dns-cname"></a>

If you have a registered domain, you can add a DNS CNAME entry to point to the Amazon S3 website endpoint\. For example, if you registered the domain `www.example-bucket.com`, you could create a bucket `www.example-bucket.com`, and add a DNS CNAME record that points to `www.example-bucket.com.s3-website.Region.amazonaws.com`\. All requests to `http://www.example-bucket.com` are routed to `www.example-bucket.com.s3-website.Region.amazonaws.com`\. 

For more information, see [Customizing Amazon S3 URLs with CNAMEs](VirtualHosting.md#VirtualHostingCustomURLs)\. 

## Using a Custom Domain with Route 53<a name="custom-domain-s3-endpoint"></a>

Instead of accessing the website using an Amazon S3 website endpoint, you can use your own domain registered with Amazon Route 53 to serve your content—for example, `example.com`\. You can use Amazon S3 with Route 53 to host a website at the root domain\. For example, if you have the root domain `example.com` and you host your website on Amazon S3, your website visitors can access the site from their browser by entering either `http://www.example.com` or `http://example.com`\. 

For an example walkthrough, see [Example: Setting Up a Static Website Using a Custom Domain Name Registered with Route 53](website-hosting-custom-domain-walkthrough.md)\. 

## Key Differences Between a Website Endpoint and a REST API Endpoint<a name="WebsiteRestEndpointDiff"></a>

An Amazon S3 website endpoint is optimized for access from a web browser\. The following table summarizes the key differences between a REST API endpoint and a website endpoint\. 


| Key Difference | REST API Endpoint | Website Endpoint | 
| --- | --- | --- | 
| Access control |  Supports both public and private content  | Supports only publicly readable content  | 
| Error message handling |  Returns an XML\-formatted error response  | Returns an HTML document | 
| Redirection support |  Not applicable  | Supports both object\-level and bucket\-level redirects | 
| Requests supported  |  Supports all bucket and object operations  | Supports only GET and HEAD requests on objects | 
| Responses to GET and HEAD requests at the root of a bucket | Returns a list of the object keys in the bucket | Returns the index document that is specified in the website configuration | 
| Secure Sockets Layer \(SSL\) support | Supports SSL connections | Does not support SSL connections | 

For a complete list of Amazon S3 endpoints, see [Amazon S3 Service Endpoints and Quotas](https://docs.aws.amazon.com/general/latest/gr/s3.html) in the *AWS General Reference*\.