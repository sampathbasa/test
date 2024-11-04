```
- name: Replace image URI in task definition
      run: |
        sed -i 's|{{IMAGE_URI}}|'"$IMAGE_URI"'|g' ecs-task-def.json
```
