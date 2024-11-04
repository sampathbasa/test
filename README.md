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
