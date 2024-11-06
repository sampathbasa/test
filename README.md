```
- name: Start SSM Session and Run Commands
        env:
          EC2_INSTANCE_ID: ${{ secrets.EC2_INSTANCE_ID }}
        run: |
          # Pull Docker image on EC2 instance
          aws ssm send-command \
            --document-name "AWS-RunShellScript" \
            --targets "Key=instanceids,Values=${EC2_INSTANCE_ID}" \
            --parameters 'commands=["sudo docker pull yourdockerusername/yourimage:latest"]' \
            --comment "Pull Docker image"

          # Run Docker container on EC2 instance
          aws ssm send-command \
            --document-name "AWS-RunShellScript" \
            --targets "Key=instanceids,Values=${EC2_INSTANCE_ID}" \
            --parameters 'commands=["sudo docker run -d -p 80:80 yourdockerusername/yourimage:latest"]' \
            --comment "Run Docker container"
```
