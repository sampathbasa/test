```
 - name: Register new task definition
      id: register-task
      run: |
        # Register task definition from file and capture the new ARN
        TASK_DEF_ARN=$(aws ecs register-task-definition \
          --cli-input-json file://ecs-task-definition.json \
          --query 'taskDefinition.taskDefinitionArn' \
          --output text)
        echo "task_definition_arn=$TASK_DEF_ARN" >> $GITHUB_ENV

    - name: Update ECS service
      run: |
        aws ecs update-service \
          --cluster your-cluster-name \
          --service your-service-name \
          --task-definition ${{ env.task_definition_arn }}
```

```
# Variables
CLUSTER_NAME="<your-cluster-name>"
SERVICE_NAME="<your-service-name>"
NEW_IMAGE_URI="<account-id>.dkr.ecr.<region>.amazonaws.com/<repository-name>:<tag>"

# Step 1: Get the latest task definition ARN for the ECS service
CURRENT_TASK_DEF_ARN=$(aws ecs describe-services \
  --cluster "$CLUSTER_NAME" \
  --services "$SERVICE_NAME" \
  --query "services[0].taskDefinition" \
  --output text)

# Step 2: Fetch the current task definition JSON
aws ecs describe-task-definition \
  --task-definition "$CURRENT_TASK_DEF_ARN" \
  --query "taskDefinition" \
  --output json > current-task-def.json

# Step 3: Replace the image in the task definition JSON file
# Using `jq` to modify the JSON with the new image URI.
UPDATED_TASK_DEF_JSON=$(jq --arg IMAGE "$NEW_IMAGE_URI" \
  '.containerDefinitions[0].image = $IMAGE' current-task-def.json)

# Save the updated JSON to a new file
echo "$UPDATED_TASK_DEF_JSON" > updated-task-def.json

# Step 4: Register the new task definition
NEW_TASK_DEF_ARN=$(aws ecs register-task-definition \
  --cli-input-json file://updated-task-def.json \
  --query "taskDefinition.taskDefinitionArn" \
  --output text)

# Step 5: Update the ECS service to use the new task definition
aws ecs update-service \
  --cluster "$CLUSTER_NAME" \
  --service "$SERVICE_NAME" \
  --task-definition "$NEW_TASK_DEF_ARN"

# Cleanup: Optional, remove temporary files
rm current-task-def.json updated-task-def.json

echo "Deployment updated with new image: $NEW_IMAGE_URI"
```
