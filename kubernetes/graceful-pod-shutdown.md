# Graceful Pod Shutdown

> Cases to avoid for graceful shutdown of pods
> 1. Pods being sent requests while shutting down
> 2. Pods being terminated while in processing for requests already Received

## 1. pods being sent requests while shutting down
Termination processing for the containers begins, removing routing rule for the pod in parallel, 
which means some traffic can be routed due to the nature of distributed system.

This can be handled by configuring `pre-stop` handler in the pod's YAML.

```yaml
spec:
  containers:
    - name: "your-container"
      image: "your-image"
      lifecycle:
        preStop:
          exec:
            command: ["sh", "-c", "sleep 10"]
```
This hook makes room for getting rid of the routing rule in advance. 
Having finished Pre-stop action, `SIGTERM` is sent to the container and graceful shutdown begins.

## 2. Pods being terminated while in processing for requests already Received
Note that you need to configure how your application handles shutdown receiving SIGTERM.  
For example, if Spring boot application is running in the pod, this properties should be configured in the YAML in Spring
or the default setting shuts it down immediately.

```yaml
server:
  shutdown: "graceful"

spring:
  lifecycle:
    timeout-per-shutdown-phase: "50s"
```

Since SIGTERM, it waits for `terminationGracePeriodSeconds` in the pod's YAML and then send `SIGKILL` to the pod.  
So, time setting for pre-stop and application's gracefulness should not only be long enough to finish processing remaining requests but also shorter than terminationGracePeriodSeconds.

```yaml
spec:
  containers:
    - name: "your-container"
      image: "your-image"
      lifecycle:
        preStop: 
          exec:
            command: ["sh", "-c", "sleep 10"]
  terminationGracePeriodSeconds: 60
```
