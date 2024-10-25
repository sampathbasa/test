```python
pip install boto3

import boto3

# Initialize the S3 client
s3 = boto3.client('s3')

# Upload the file
file_path = "path/to/your/local/file"
bucket_name = "your-bucket-name"
s3_key = "folder/in/bucket/filename.ext"

try:
    s3.upload_file(file_path, bucket_name, s3_key)
    print(f"File uploaded to S3://{bucket_name}/{s3_key}")
except Exception as e:
    print(f"An error occurred: {e}")
