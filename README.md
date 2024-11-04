```
- name: Replace image URI in task definition
      run: |
        sed -i 's|{{IMAGE_URI}}|'"$IMAGE_URI"'|g' ecs-task-def.json
```
https://docs.github.com/en/actions/use-cases-and-examples/deploying/deploying-to-amazon-elastic-container-service

GitHub-hosted runners need open access to AWS ECS and ECR endpoints over HTTPS.


