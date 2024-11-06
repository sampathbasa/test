```
- name: Check SSM Command Status
  run: |
    COMMAND_ID=$(aws ssm list-commands --filters Key=InstanceId,Values=${{ env.EC2_INSTANCE_ID }} --query 'Commands[0].CommandId' --output text)
    aws ssm get-command-invocation --command-id "$COMMAND_ID" --instance-id "${{ env.EC2_INSTANCE_ID }}"

```
