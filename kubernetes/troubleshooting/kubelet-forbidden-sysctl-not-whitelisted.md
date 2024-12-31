# kubelet forbidden sysctl: not whitelisted

> `kubelet --allowed-unsafe-sysctls` flag has been deprecated.  
> 
> There are safe and unsafe sysctls allowed in kubelet config.  
> Safe sysctls are enabled as the default but unsafe sysctls are not.  
> To enable an unsafe sysctl, it needs to be added to the config in the worker nodes.


## 1. Find kubelet configuration file path
```shell
systemctl status kubelet
```
After that command, find the argument for `--config` option which is the kubelet config file path.

## 2. Add the Unsafe Sysctl to the Config file
```yaml
apiVersion: kubelet.config.k8s.io/v1beta1
kind: KubeletConfiguration
...
allowedUnsafeSysctls:
- "net.ipv4.tcp_keepalive_time"
```
For this example, `net.ipv4.tcp_keepalive_time` has been added.

## 3. Restart kubelet
```shell
systemctl restart kubelet
```
Restart kubelet to apply the change in the config.
