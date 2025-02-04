# How Min-Ready-Seconds and Readiness-Probe Work Together

> `readinessProbe` ignores `.spec.minReadySeconds` and gets traffic, 
> having done the probe even if minReadySeconds still has remaining time.
> 
> minReadySeconds defaults to 0.
> 
> Note that minReadySeconds is a good choice 
> when the application for the pod is not suitable for readinessProbe setting.