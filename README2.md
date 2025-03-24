# Deploying a static website to an Amazon S3 bucket using the AWS Command Line Interface (CLI) involves several steps. Here’s a comprehensive guide to help you through the process.

### Prerequisites

1. **AWS Account**: You need to have an AWS account. If you don’t have one, you can sign up at the [AWS website](https://aws.amazon.com/).

2. **Install AWS CLI**: Make sure the AWS CLI is installed on your machine. You can download and install it from the [AWS CLI installation guide](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-quickstart.html).

3. **Configure AWS CLI**: After installation, configure the CLI with your AWS credentials using the following command:
   ```bash
   aws configure
   ```
   You will be prompted for your AWS Access Key ID, Secret Access Key, default region name, and output format.

4. **Static Website Files**: Prepare the files for your static website (e.g., HTML, CSS, JavaScript, images).

### Step-by-Step Guide to Deploy a Static Website to S3

#### Step 1: Create an S3 Bucket

1. **Create a Bucket**: Use the following command to create an S3 bucket. Replace `your-bucket-name` with a globally unique name for your bucket:
   ```bash
   aws s3api create-bucket --bucket your-bucket-name --region your-region --create-bucket-configuration LocationConstraint=your-region
   ```
   For example, if you are using `eu-north-1`, the command will look like:
   ```bash
   aws s3api create-bucket --bucket your-bucket-name --region us-east-1
   ```
![alt text](<Screenshot 2025-03-16 124243.png>)
2. **Enable Static Website Hosting**: Configure your bucket for static website hosting:
   ```bash
   aws s3 website s3://your-bucket-name --index-document index.html --error-document error.html
   ```
   ![alt text](<Screenshot 2025-03-16 125003.png>)

#### Step 2: Upload Your Website Files

1. **Copy Files to S3**: Use the following command to sync your local website directory to your S3 bucket. Replace `path/to/your/website/*` with the path to your website files:
   ```bash
   aws s3 sync path/to/your/website/ s3://your-bucket-name/
   ```
![alt text](<Screenshot 2025-03-16 183508.png>)

#### Step 3: To turn on public access
To turn on public access to an Amazon S3 bucket using the AWS Command Line Interface (CLI), you can use the  command. Amazon S3 provides a set of public access settings that can be configured to help block public access to your S3 buckets.
Command to Turn Off Public Access is
 ```bash
 aws s3api put-public-access-block --bucket your-bucket-name --public-access-block-configuration "BlockPublicAcls=false,IgnorePublicAcls=false,BlockPublicPolicy=false,RestrictPublicBuckets=false"
 ```
 ![alt text](<Screenshot 2025-03-16 172559.png>)

#### Step 3: Set Bucket Policy for Public Access

1. **Set Bucket Policy**: Allow public access to the files in your S3 bucket by creating a policy. You can create a file named `policy2.json` , open in vscode using `code .` the following content:

   ```json
   {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Sid": "PublicReadGetObject",
               "Effect": "Allow",
               "Principal": "*",
               "Action": "s3:GetObject",
               "Resource": "arn:aws:s3:::your-bucket-name/*"
           }
       ]
   }
   ```
   ![alt text](<Screenshot 2025-03-16 170315.png>)
   ![alt text](<Screenshot 2025-03-16 170652.png>)

2. **Apply the Policy**: Use the following command to apply the policy:
   ```bash
   aws s3api put-bucket-policy --bucket your-bucket-name --policy file://policy2.json
   ```

#### Step 4: Access Your Website

1. **Get the Website URL**: Your website can be accessed using the following URL format:
   ```
   http://your-bucket-name.s3-website-your-region.amazonaws.com
   ```
   Replace `your-bucket-name` and `your-region` with your respective values.

### Example of the Complete Commands

Here is a summary of all the commands you need to run, assuming your bucket name is `my-static-site` and you're using the `us-west-2` region:

```bash
# Step 1: Create Bucket
aws s3api create-bucket --bucket my-static-site --region us-west-2 --create-bucket-configuration LocationConstraint=us-west-2

# Step 2: Enable Static Website Hosting
aws s3 website s3://my-static-site --index-document index.html --error-document error.html

# Step 3: Upload Files
aws s3 sync ./path/to/your/website/ s3://my-static-site/

# Step 4: Set Bucket Policy
# Create `bucket-policy.json` with the appropriate content

aws s3api put-bucket-policy --bucket my-static-site --policy file://bucket-policy.json

# Access the site
# http://my-static-site.s3-website-us-west-2.amazonaws.com
```
