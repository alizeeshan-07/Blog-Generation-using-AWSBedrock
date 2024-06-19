# Blog Generation using Bedrock

**Overview**

This script generates a blog post using the Bedrock AI model and saves it to an AWS S3 bucket.

![Blog-Generation-With-AWS-Bedrock](https://github.com/alizeeshan-07/Blog-Generation-using-AWSBedrock/assets/70628992/bf0f8b76-0ad3-4562-8760-538f50267833)


**Requirements**

- Python 3.10+
- **boto3** library (`pip install boto3`)

**Setup**

1. **AWS Setup:**
   - Ensure you have an AWS account set up.
   - Configure AWS credentials with appropriate permissions to access S3 and Bedrock services.

2. **Python Environment:**
   - Install the required dependencies using `pip`:
     ```
     pip install boto3
     ```

**Usage**

1. **Lambda Configuration:**
   - Create an AWS Lambda function with the following configuration:
     - **Runtime:** Python 3.11+
     - **Handler:** `lambda_handler.lambda_handler`
     - **Trigger:** HTTP API Gateway (or other HTTP trigger)

2. **HTTP Request Format:**
   - Send an HTTP POST request to the Lambda endpoint with the following JSON payload:
     ```json
     {
       "blog_topic": "Your Blog Topic Here"
     }
     ```

3. **Output:**
   - The generated blog post will be saved as a text file in the specified S3 bucket (`aws_bedrock_blog_app`) under the `blog_output` directory.

**Function Details**

- **`blog_generate_using_bedrock(blogtopic:str) -> str`:**
  - Generates a blog post using the specified `blogtopic` with parameters configured for the Bedrock AI model.

- **`save_blog_details_s3(s3_key, s3_bucket, generate_blog)`:**
  - Saves the generated blog content (`generate_blog`) to the specified S3 bucket (`s3_bucket`) with the key (`s3_key`).

- **`lambda_handler(event, context)`:**
  - Entry point for AWS Lambda function.
  - Extracts `blog_topic` from the incoming HTTP POST request.
  - Calls `blog_generate_using_bedrock` to generate the blog post.
  - Saves the generated blog to S3 using `save_blog_details_s3`.

**Notes**

- Ensure proper AWS IAM permissions are set for the Lambda function to access S3 and Bedrock services.
- Monitor AWS CloudWatch logs for debugging and operational insights.
