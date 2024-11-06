```
- name: Start SSM Session and Run Commands
        run: |
          # Pull and Run Docker image on EC2 instance
          aws ssm send-command \
            --document-name "AWS-RunShellScript" \
            --targets "Key=instanceids,Values=${{ env.EC2_INSTANCE_ID }}" \
            --parameters '{"commands": [
              "docker pull ${{ env.ECR_REGISTRY }}/${{ env.ECR_REPOSITORY }}:${{ env.TAG_APP }}",
              "docker ps",
              "docker images",
              "docker run -d -p 3010:80 --name emcx-fe-dev ${{ env.ECR_REGISTRY }}/${{ env.ECR_REPOSITORY }}:${{ env.TAG_APP }}",
              "docker ps",
              "docker images"
            ]}' \
            --comment "Pull and Run Docker image on EC2 instance"
```
