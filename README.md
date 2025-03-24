# github-work
## HOW TO DEPLOY A STATIC WEBSITE TO AN AMASON S3 BUCKET USING AWS MANAGEMENT CONSOLE 

### Prerequisites

- **An AWS account** You need to have an AWS account. If you don’t have one, you can sign up at the [AWS website](https://aws.amazon.com/).
- Your code or use a ready-starter-code - Download to your  local computer and unzip the folder
- AWS region used is eu-north-1
 
 ### What is Amazon S3 Bucket
S3 Buckets are public cloud storage containers for objects stored in Amazon Simple Storage Service (S3). Object storage is a type of data storage architecture that manages and organizes data as discrete units called objects. In this storage model, data is stored as individual objects, each with its unique identifier, metadata, and data content. These objects can be files, images, videos, documents, or any other form of unstructured or semi-structured data.


### Create S3 Bucket
1.  Navigate to the “AWS Management Console” page, click on  “Services”, click on “Storage”, click on “S3"

![alt text](<Screenshot 2025-03-14 220556.png>)

2. The Amazon S3 dashboard displays. Click “Create bucket”

![alt text](<Screenshot 2025-03-14 220954.png>)
3. In the General configuration, enter a “Bucket name” and a region of your choice. Note: Bucket names must be globally unique.![alt text](<Screenshot 2025-03-14 221139.png>)

4. In the Bucket settings for the Block Public Access section, uncheck the “Block all public access”. It will enable public access to the bucket objects via the S3 object URL. Check the acknowledgement button. Click “Create bucket”
![alt text](<Screenshot 2025-03-14 221230.png>)


### Upload files to S3 Bucket

1. The bucket has been created. Click the “Bucket name”
![alt text](<Screenshot 2025-03-14 222250.png>)

2. once the bucket is open to its contents, click the “Upload” button. Click the "Add files" button, and upload the  file content from your local computer to the S3 bucket. Click upload
![alt text](<Screenshot 2025-03-14 222401.png>)

![alt text](<Screenshot 2025-03-14 222507.png>)
![alt text](<Screenshot 2025-03-14 222856.png>)

### Secure Bucket

1. Click on the “Permissions” tab.


2. The “Bucket Policy” section shows it is empty. Click on the Edit button.

3. Enter the following bucket policy replacing “monsi-bucket1” with the name of your bucket and click “Save”.
![alt text](<Screenshot 2025-03-14 230447.png>)
You will see warnings about making your bucket public, but this step is required for static website hosting

### Configure S3 Bucket
Go to the Properties tab and then scroll down to edit the Static website hosting section.


Click on the “Edit” button to see the Edit static website hosting screen. Now, enable the Static website hosting. The Hosting type should be “Host a Static Website”. For both “Index document” and “Error document”, enter “index.html” and click “Save”.
![alt text](<Screenshot 2025-03-14 223843.png>)




After successfully saving the settings, check the Static website hosting section again under the Properties tab. You must now be able to view the website endpoint as shown below:
![alt text](<Screenshot 2025-03-15 102301.png>)







