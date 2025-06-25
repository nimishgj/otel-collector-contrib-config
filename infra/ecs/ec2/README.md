

Run the task definition as a daemon service with launch type ec2 

For the application use the below log configuration:
```
"logConfiguration": {
        "logDriver": "awsfirelens",
        "options": {
          "Host": "172.17.0.1",
          "Name": "forward",
          "Port": "8006"
        }
}
```


and add a sidecar with the application
```json
{
      "name": "log_router",
      "image": "public.ecr.aws/aws-observability/aws-for-fluent-bit:stable",
      "cpu": 0,
      "memoryReservation": 51,
      "portMappings": [],
      "essential": true,
      "environment": [],
      "mountPoints": [],
      "volumesFrom": [],
      "user": "0",
      "logConfiguration": {
        "logDriver": "json-file"
      },
      "systemControls": [],
      "firelensConfiguration": {
        "type": "fluentbit"
      }
    }
```
