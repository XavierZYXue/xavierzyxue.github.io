# PoC result
```
for i in {1..10} ; do curl localhost:8080 ; done
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
<html><body><h1>It works!</h1></body></html>
<html><body><h1>It works!</h1></body></html>
<html><body><h1>It works!</h1></body></html>
<html><body><h1>It works!</h1></body></html>
<html><body><h1>It works!</h1></body></html>
<html><body><h1>It works!</h1></body></html>
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
<html><body><h1>It works!</h1></body></html>
<html><body><h1>It works!</h1></body></html>
```
# k8s cluster
```
kubectl get po
NAME                            READY   STATUS    RESTARTS      AGE
wonderful-v1-74cffc64c9-26skl   1/1     Running   1 (43m ago)   79m
wonderful-v2-dbf975874-h5vml    1/1     Running   1 (43m ago)   79m

kubectl get svc
NAME           TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)   AGE
kubernetes     ClusterIP   10.43.0.1       <none>        443/TCP   79m
wonderful-v1   ClusterIP   10.43.83.176    <none>        80/TCP    79m
wonderful-v2   ClusterIP   10.43.146.197   <none>        80/TCP    79m

kubectl get ing
NAME                       CLASS   HOSTS       ADDRESS      PORTS   AGE
wonderful-ingress-canary   nginx   localhost   172.19.0.5   80      78m
wonderful-ingress-v1       nginx   localhost   172.19.0.5   80      79m
```
# app1
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: wonderful
    version: v1
  name: wonderful-v1
spec:
  replicas: 1
  selector:
    matchLabels:
      app: wonderful
      version: v1
  template:
    metadata:
      labels:
        app: wonderful
        version: v1
    spec:
      containers:
      - image: httpd:alpine
        name: httpd
```

# service1
```yaml
apiVersion: v1
kind: Service
metadata:
  labels:
    app: wonderful
    version: v1
  name: wonderful-v1
spec:
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
  selector:
    app: wonderful
    version: v1
  type: ClusterIP
```

# ingress1
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: wonderful-ingress-v1
  annotations:
    # nginx.ingress.kubernetes.io/rewrite-target: /
    # nginx.ingress.kubernetes.io/backend-protocol: "HTTP"
    # ingress.kubernetes.io/ssl-redirect: "false"
spec:
  ingressClassName: nginx
  rules:
  - host: localhost
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: wonderful-v1
            port:
              number: 80
```

# app2
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: wonderful
    version: v2
  name: wonderful-v2
spec:
  replicas: 1
  selector:
    matchLabels:
      app: wonderful
      version: v2
  template:
    metadata:
      labels:
        app: wonderful
        version: v2
    spec:
      containers:
      - image: nginx:alpine
        name: nginx
```

# service2
```yaml
apiVersion: v1
kind: Service
metadata:
  labels:
    app: wonderful
    version: v2
  name: wonderful-v2
spec:
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
  selector:
    app: wonderful
    version: v2
  type: ClusterIP
```

# ingress2
```yaml
# 金丝雀版本的 Ingress
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: wonderful-ingress-canary
  annotations:
    # 启用金丝雀发布
    # nginx.ingress.kubernetes.io/rewrite-target: /
    # 金丝雀发布配置 - 10% 流量导向 v2
    nginx.ingress.kubernetes.io/canary: "true"
    nginx.ingress.kubernetes.io/canary-weight: "10"
    # 可选：基于请求头的金丝雀发布
    # nginx.ingress.kubernetes.io/canary-by-header: "Canary"
    # nginx.ingress.kubernetes.io/canary-by-header-value: "true"
    # 可选：基于 Cookie 的金丝雀发布
    # nginx.ingress.kubernetes.io/canary-by-cookie: "canary"
spec:
  ingressClassName: nginx
  rules:
  - host: localhost
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: wonderful-v2
            port:
              number: 80
```