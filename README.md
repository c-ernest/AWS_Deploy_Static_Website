# AWS_Deploy_Static_Website
Cloud is perfect for hosting static websites that only include HTML, CSS, and JavaScript files that require no server-side processing. 
This project has two major intentions to implement:

Hosting a static website on S3 and
Accessing the cached website pages using CloudFront content delivery network (CDN) service.

## Resources and Steps to deploy with S3
- You need to create an account with AWS and login
- Create an s3 bucket (bucket name must be globally unique)
- Configure your bucket to be publicly accessible 
- Upload your website files to the bucket (ensure your home page/index.html is in the root bucket)
- Next, secure your bucket via IAM by allow public access on the permission tab
- Also remember to enter the following bucket policy and replace 'your-website' with your bucket name and save
{
"Version":"2012-10-17",
"Statement":[
 {
   "Sid":"AddPerm",
   "Effect":"Allow",
   "Principal": "*",
   "Action":["s3:GetObject"],
   "Resource":["arn:aws:s3:::your-website/*"]
 }
]
}
- Next, Click on the “Edit” button to enable the Static website hosting, and provide the default home page and error page for your website
- Copy the website endpoint and paste on a browser -- viola! Your langing page is ready.

## With Cloudfront
- Search for cloudfront from the services and create distribution from cloudfront dashboard.
- For “Select a delivery method for your content”, click “Get Started”.
- Use the following details to create a distribution:
Field	Value
- Origin > Domain Name: Paste the Static website hosting endpoint of the form <bucket-name>.s3-website-region.amazonaws.com
- Origin > Enable Origin Shield	No
- Default cache behavior	Use default settings	
- Cache key and origin requests	Use default settings
- Configurations - Origin details
- Configurations - Cache behavior, key and origin requests
- Leave the defaults for the rest of the options, and click “Create Distribution”. 
- Once the status of your distribution changes from “In Progress” to “Deployed”, copy the endpoint URL for your CloudFront distribution found in the “Domain Name” column.

## Access Website in Web Browser
Note - the exact domain name and the S3 URLs will be different in your case.

Open a web browser like Google Chrome, and paste the copied CloudFront domain name (such as, dgf7z6g067r6d.cloudfront.net) without appending /index.html at the end. The CloudFront domain name should show you the content of the default home-page, as shown below:
