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

