# Resource detection processor for AWS EKS

```yaml
processors:
  resourcedetection/eks:
    detectors: [env, eks]
    timeout: 15s
    override: false
    eks:
      resource_attributes:
        cloud.account.id:
          enabled: true
        cloud.platform:
          enabled: true
        cloud.provider:
          enabled: true
        k8s.cluster.name:
          enabled: true
```
