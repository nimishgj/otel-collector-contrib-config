# k8attributes processor to add every possible supported attributes

```yaml
k8sattributes:
  auth_type: 'serviceAccount'
    extract:
      metadata:
        - k8s.namespace.name
        - k8s.pod.name
        - k8s.pod.hostname
        - k8s.pod.ip
        - k8s.pod.start_time
        - k8s.pod.uid
        - k8s.replicaset.uid
        - k8s.replicaset.name
        - k8s.deployment.uid
        - k8s.deployment.name
        - k8s.daemonset.uid
        - k8s.daemonset.name
        - k8s.statefulset.uid
        - k8s.statefulset.name
        - k8s.cronjob.uid
        - k8s.cronjob.name
        - k8s.job.uid
        - k8s.job.name
        - k8s.node.name
        - k8s.cluster.uid
        - container.image.name
        - container.image.tag
        - container.id

      annotations:
        - tag_name: service.name
          key: resource.opentelemetry.io/service.name
          from: pod
        - tag_name: service.namespace
          key: resource.opentelemetry.io/service.namespace
          from: pod
        - tag_name: service.version
          key: resource.opentelemetry.io/service.version
          from: pod
        - tag_name: service.instance.id
          key: resource.opentelemetry.io/service.instance.id
          from: pod
      labels:
          - tag_name: kube_app_name
            key: app.kubernetes.io/name
            from: pod
          - tag_name: kube_app_instance
            key: app.kubernetes.io/instance
            from: pod
          - tag_name: kube_app_version
            key: app.kubernetes.io/version
            from: pod
          - tag_name: kube_app_component
            key: app.kubernetes.io/component
            from: pod
          - tag_name: kube_app_part_of
            key: app.kubernetes.io/part-of
            from: pod
          - tag_name: kube_app_managed_by
            key: app.kubernetes.io/managed-by
            from: pod
      pod_association:
        - sources:
            - from: resource_attribute
              name: k8s.pod.ip
        - sources:
            - from: resource_attribute
              name: k8s.pod.uid
        - sources:
            - from: connection

```
