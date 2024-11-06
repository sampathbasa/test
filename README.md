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

```
- name: Set up SSH key
        run: |
          echo "${{ secrets.EC2_SSH_KEY }}" > private_key.pem
          chmod 600 private_key.pem

      - name: SSH into EC2 and run commands
        run: |
          ssh -tt -o StrictHostKeyChecking=no -i private_key.pem ec2-user@${{ secrets.EC2_INSTANCE_PUBLIC_IP }} << 'EOF'
            # Add your deployment commands here
            echo "Running deployment on EC2..."
            # Example:
            sudo systemctl restart my-application.service
          EOF

      - name: Clean up SSH key
        run: rm -f private_key.pem
```
