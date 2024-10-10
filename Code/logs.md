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

=================

@rifaterdemsahin ➜ /workspaces/thanoswithdocker (main) $ kubectl logs my-release-thanos-query-6cf69d9499-48hw9 -n monitoring-testing-october24
ts=2024-10-10T14:49:53.899948648Z caller=options.go:26 level=info protocol=gRPC msg="disabled TLS, key and cert must be set to enable"
ts=2024-10-10T14:49:53.901631657Z caller=query.go:833 level=info msg="starting query node"
ts=2024-10-10T14:49:53.902314324Z caller=intrumentation.go:75 level=info msg="changing probe status" status=healthy
ts=2024-10-10T14:49:53.902345725Z caller=http.go:73 level=info service=http/server component=query msg="listening for requests and metrics" address=0.0.0.0:10902
ts=2024-10-10T14:49:53.9036216Z caller=tls_config.go:313 level=info service=http/server component=query msg="Listening on" address=[::]:10902
ts=2024-10-10T14:49:53.90364962Z caller=tls_config.go:316 level=info service=http/server component=query msg="TLS is disabled." http2=false address=[::]:10902
ts=2024-10-10T14:49:53.903718255Z caller=intrumentation.go:56 level=info msg="changing probe status" status=ready
ts=2024-10-10T14:49:53.903751623Z caller=grpc.go:167 level=info service=gRPC/server component=query msg="listening for serving gRPC" address=0.0.0.0:10901

====================================================================================================================

TLS is disabled." http2=false address=[::]:10902
=======================================================================================================================
@rifaterdemsahin ➜ /workspaces/thanoswithdocker (main) $ kubectl logs my-release-thanos-query-frontend-55c47f5b95-mfpfk -n monitoring-testing-october24
ts=2024-10-10T14:49:53.661187388Z caller=query_frontend.go:386 level=info msg="starting query frontend"
ts=2024-10-10T14:49:53.662123488Z caller=intrumentation.go:56 level=info msg="changing probe status" status=ready
ts=2024-10-10T14:49:53.665304021Z caller=intrumentation.go:75 level=info msg="changing probe status" status=healthy
ts=2024-10-10T14:49:53.665340891Z caller=http.go:73 level=info service=http/server component=query-frontend msg="listening for requests and metrics" address=0.0.0.0:9090
ts=2024-10-10T14:49:53.666311028Z caller=tls_config.go:313 level=info service=http/server component=query-frontend msg="Listening on" address=[::]:9090
ts=2024-10-10T14:49:53.671125579Z caller=tls_config.go:316 level=info service=http/server component=query-frontend msg="TLS is disabled." http2=false address=[::]:9090

=================================================

