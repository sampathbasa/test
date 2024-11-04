```
- name: Replace image URI in task definition
      run: |
        sed -i 's|{{IMAGE_URI}}|'"$IMAGE_URI"'|g' ecs-task-def.json
```
https://docs.github.com/en/actions/use-cases-and-examples/deploying/deploying-to-amazon-elastic-container-service

GitHub-hosted runners need open access to AWS ECS and ECR endpoints over HTTPS.


Hi GitHub Support Team,

I am encountering an issue with deploying an application to my AWS ECS service through GitHub Actions. The deployment process fails due to an "ECS connection timeout" error. From what I understand, GitHub Actions runners require open HTTPS access to AWS ECS and ECR endpoints for deployments to succeed.
