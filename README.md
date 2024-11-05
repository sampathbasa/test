```
 - name: SSH into EC2 and Deploy
      env:
        IMAGE_URI: ${{ secrets.ECR_REGISTRY }}/${{ secrets.ECR_REPOSITORY }}:latest
      run: |
        # Assuming you have SSH access and your EC2 instance is configured to allow SSH
        ssh -o StrictHostKeyChecking=no -i ${{ secrets.EC2_SSH_KEY }} ec2-user@${{ secrets.EC2_INSTANCE_PUBLIC_IP }} << 'EOF'
          # Pull the latest Docker image
          sudo docker pull $IMAGE_URI

          # Stop and remove the existing container
          sudo docker stop my-app || true
          sudo docker rm my-app || true
```
