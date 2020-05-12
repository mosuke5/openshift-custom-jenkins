# Example of custom jenkins on OpenShift

## How to build custom jenkins image
```
$ oc new-project admin-devops
$ oc apply -f example-manifest.yaml
$ oc start-build custom-jenkins-build
```

## How to deploy Jenkins
```
oc process --param JENKINS_IMAGE_STREAM_TAG=custom-jenkins:latest --param NAMESPACE=admin-devops --param ENABLE_OAUTH=true --param MEMORY_LIMIT=4Gi --param CPU_LIMIT=2000m --param VOLUME_CAPACITY=10Gi --param DISABLE_ADMINISTRATIVE_MONITORS=true -f template.yaml | oc apply -f -
```
