# Example of custom jenkins on OpenShift

- add plugins (`plugins.txt`)
- add sample-job (`configuration/jobs/sample-job/config.xml`)

## How to build custom jenkins image
```
$ oc new-project admin-devops
$ oc apply -f example-manifest.yaml
buildconfig.build.openshift.io/custom-jenkins created
imagestream.image.openshift.io/custom-jenkins created buildconfig.build.openshift.io/custom-jenkins-agent created
imagestream.image.openshift.io/custom-jenkins-agent created

$ oc start-build custom-jenkins
$ oc get pod
NAME                     READY   STATUS      RESTARTS   AGE
custom-jenkins-1-build   0/1     Completed   0          28m
```

## How to deploy Jenkins
After building your custom jenkins image, you can deploy it.

```
$ oc process --param JENKINS_IMAGE_STREAM_TAG=custom-jenkins:latest --param NAMESPACE=admin-devops --param ENABLE_OAUTH=true --param MEMORY_LIMIT=4Gi --param CPU_LIMIT=2000m --param VOLUME_CAPACITY=10Gi --param DISABLE_ADMINISTRATIVE_MONITORS=true -f template.yaml | oc apply -f -
```

## How to build custom jenkins agent
When you want to build your customized jenkins agent image, you can build it easily.

```
$ oc apply -f example-manifest.yaml
buildconfig.build.openshift.io/custom-jenkins created
imagestream.image.openshift.io/custom-jenkins created
buildconfig.build.openshift.io/custom-jenkins-agent created
imagestream.image.openshift.io/custom-jenkins-agent created

$ oc start-build custom-jenkins-agent
-> build from 'Dockerfile_for_agent' 
```
