# p-14653-1-mission
- 0015 완료

---

early@JAKEPARK-MAINPC MINGW64 ~
$ vi namespace.yaml

early@JAKEPARK-MAINPC MINGW64 ~
$ vi namespace.yaml

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl apply -f namespace.yaml
namespace/demo-app created

early@JAKEPARK-MAINPC MINGW64 ~
$ vi backend-deployment.yaml

early@JAKEPARK-MAINPC MINGW64 ~
$ vi frontend-deployment.yaml:

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl apply -f namespace.yaml
namespace/demo-app unchanged

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl apply -f backend-deployment.yaml
deployment.apps/backend created
service/backend-service created

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl apply -f frontend-deployment.yaml
error: the path "frontend-deployment.yaml" does not exist

early@JAKEPARK-MAINPC MINGW64 ~
$ vi frontend-deployment.yaml

early@JAKEPARK-MAINPC MINGW64 ~
$ rm frontend-deployment.yaml:

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl apply -f frontend-deployment.yaml
deployment.apps/frontend created
service/frontend-service created

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl get all -n demo-app
NAME                            READY   STATUS    RESTARTS   AGE
pod/backend-746f6d7d4d-hn5t6    1/1     Running   0          45s
pod/backend-746f6d7d4d-t4mdg    1/1     Running   0          45s
pod/frontend-7d84cb49b6-7pd8p   1/1     Running   0          7s
pod/frontend-7d84cb49b6-zf6qk   1/1     Running   0          7s

NAME                       TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)        AGE
service/backend-service    ClusterIP      10.96.92.197     <none>        8080/TCP       45s
service/frontend-service   LoadBalancer   10.102.174.249   localhost     80:31341/TCP   7s

NAME                       READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/backend    2/2     2            2           45s
deployment.apps/frontend   2/2     2            2           8s

NAME                                  DESIRED   CURRENT   READY   AGE
replicaset.apps/backend-746f6d7d4d    2         2         2       45s
replicaset.apps/frontend-7d84cb49b6   2         2         2       7s

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl exec -n demo-app -it \
  $(kubectl get pod -n demo-app -l app=frontend -o jsonpath='{.items[0].metadata.name}') \
  -- curl backend-service:8080
Hello from Backend!

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl delete namespace demo-app
namespace "demo-app" deleted
