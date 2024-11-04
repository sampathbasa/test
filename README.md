 ```
     - name: Update ECS service with new image
        env:
          CLUSTER_NAME: demo-cluster1  # Replace with your ECS cluster name
          SERVICE_NAME: frontend       # Replace with your ECS service name
          IMAGE_URI: <your-account-id>.dkr.ecr.us-east-1.amazonaws.com/<your-repository-name>:${{ github.sha }}
        run: |
          aws ecs update-service --cluster $CLUSTER_NAME --service $SERVICE_NAME --force-new-deployment --desired-count 1 --region us-east-1 --cli-input-json "{\"service\": {\"containerDefinitions\": [{\"image\": \"$IMAGE_URI\"}]}}"

      - name: Confirm ECS deployment
        run: |
          aws ecs wait services-stable --cluster $CLUSTER_NAME --services $SERVICE_NAME
          echo "Deployment to ECS is complete"
```

```
aws ecs register-task-definition \
    --family your-task-family \
    --container-definitions '[{"name":"your-container-name","image":"your-image:your-new-tag","memory":512,"cpu":256,"essential":true}]'

aws ecs update-service \
    --cluster your-cluster-name \
    --service your-service-name \
    --task-definition your-task-family:revision
```

```
aws sts assume-role \
    --role-arn arn:aws:iam::account-id:role/role-name \
    --role-session-name session-name

```
#!/bin/bash

# Variables
ROLE_ARN="arn:aws:iam::123456789012:role/MyRole"  # Replace with your IAM role ARN
SESSION_NAME="MySession"  # Replace with your session name

# Assume the role and capture the output
CREDENTIALS_JSON=$(aws sts assume-role --role-arn "$ROLE_ARN" --role-session-name "$SESSION_NAME")

# Check if the assume-role command succeeded
if [ $? -ne 0 ]; then
    echo "Failed to assume role."
    exit 1
fi

# Extract the temporary security credentials
AWS_ACCESS_KEY_ID=$(echo "$CREDENTIALS_JSON" | jq -r '.Credentials.AccessKeyId')
AWS_SECRET_ACCESS_KEY=$(echo "$CREDENTIALS_JSON" | jq -r '.Credentials.SecretAccessKey')
AWS_SESSION_TOKEN=$(echo "$CREDENTIALS_JSON" | jq -r '.Credentials.SessionToken')

# Export the credentials as environment variables
export AWS_ACCESS_KEY_ID
export AWS_SECRET_ACCESS_KEY
export AWS_SESSION_TOKEN

# Optional: Print out the caller identity to verify
aws sts get-caller-identity

echo "Assumed role and exported temporary credentials."
```
