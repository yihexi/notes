dashboard token 查看

```
kubectl get secret -n kube-system | grep token
kubectl describe secret cluster-viewer-token-6k745 -n kube-system
 
kubectl get secret -n kubernetes-dashboard | grep token | grep admin
kubectl describe secret default-token-gtvsw  -n kubernetes-dashboard
```

查看pod 事件：

```
kubectl get events --field-selector involvedObject.name=vl-sync-manual-n7q-2lmhc -n inference
```

批量删除Pod

```
kubectl get pod -n asr-default | grep UnexpectedAdmissionError | awk '{print $1}' | xargs kubectl delete pod -n asr-default 
```

查看所有pod信息

 ```
docker stats --no-stream --format "table {{.Name}}\t{{.Container}}\t{{.CPUPerc}}\t{{.MemUsage}}\t{{.MemPerc}}"
 ```

查看docker是否运行在privileged权限下？

```
docker inspect --format='{{.HostConfig.Privileged}}' [container_id]
```

暂停滚动更新与恢复

```
kubectl rollout pause deployment my-deployment
kubectl get deployment my-deployment -o yaml | grep paused
kubectl rollout resume deployment my-deployment
```

drain掉机器与恢复

```
kubectl drain 172-21-194-46 --ignore-daemonsets --delete-emptydir-data
kubectl get nodes 172-21-194-46
kubectl uncordon 172-21-194-46

查看所有状态不是running的pod
kubectl get pods --all-namespaces --field-selector=status.phase!=Running
```

查看oom-kill日志

```
tail -n1000 /var/log/messages | grep -i "oom"
```

进入Pod命名空间

```
docker ps | grep xxxx
docker inspect k8s-xxxx | grep Pid
nsenter Pid
ip addresss
```

