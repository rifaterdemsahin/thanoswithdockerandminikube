@rifaterdemsahin ➜ /workspaces/thanoswithdocker (main) $  kubectl get all -n monitoring-testing-october24
NAME                                                    READY   STATUS    RESTARTS      AGE
pod/my-release-thanos-query-6cf69d9499-48hw9            1/1     Running   1 (43m ago)   100m
pod/my-release-thanos-query-frontend-55c47f5b95-mfpfk   1/1     Running   1 (43m ago)   100m

NAME                                       TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)     AGE
service/my-release-thanos-query            ClusterIP   10.100.55.144   <none>        9090/TCP    100m
service/my-release-thanos-query-frontend   ClusterIP   10.98.240.111   <none>        9090/TCP    100m
service/my-release-thanos-query-grpc       ClusterIP   10.97.31.185    <none>        10901/TCP   100m

NAME                                               READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/my-release-thanos-query            1/1     1            1           100m
deployment.apps/my-release-thanos-query-frontend   1/1     1            1           100m

NAME                                                          DESIRED   CURRENT   READY   AGE
replicaset.apps/my-release-thanos-query-6cf69d9499            1         1         1       100m
replicaset.apps/my-release-thanos-query-frontend-55c47f5b95   1         1         1       100m