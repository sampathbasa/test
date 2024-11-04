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
