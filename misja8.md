Błąd yml: 
 * ServiceAccount wiesio-admin - nie ma żadnych uprawnień.
 * kubectl get nodes - zasób cluster-scoped, potrzebny ClusterRole + ClusterRoleBinding
 * livenessProbe odpytuje /healthz - nginx:alpine tego nie serwuje, zwraca 404, liveness probe fail, nieskończone restarty
 * bitnami/kubectl:latest - tag :latest (dodatkowo blokowany przez Misję 9)
Nowy yml:
```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: panel-kierownictwa
---
apiVersion: v1
kind: ServiceAccount
metadata:
  name: wiesio-admin
  namespace: panel-kierownictwa
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: wiesio-node-reader
rules:
  - apiGroups: [""]
    resources: ["nodes"]
    verbs: ["get", "list"]
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: wiesio-node-reader-binding
subjects:
  - kind: ServiceAccount
    name: wiesio-admin
    namespace: panel-kierownictwa
roleRef:
  kind: ClusterRole
  name: wiesio-node-reader
  apiGroup: rbac.authorization.k8s.io
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: tajny-panel
  namespace: panel-kierownictwa
spec:
  replicas: 1
  selector:
    matchLabels:
      app: tajny-panel
  template:
    metadata:
      labels:
        app: tajny-panel
    spec:
      serviceAccountName: wiesio-admin
      initContainers:
        - name: system-check
          image: bitnami/kubectl:1.31.0
          command: ['sh', '-c', 'kubectl get nodes && echo "System gotowy"']
      containers:
        - name: web
          image: nginx:alpine
          ports:
            - containerPort: 80
          livenessProbe:
            httpGet:
              path: /
              port: 80
            initialDelaySeconds: 2
            periodSeconds: 2
```

Wdrażanie nowego yml:
Importowanie nowego yml w zakładce Import YAML
<img width="1438" height="681" alt="obraz" src="https://github.com/user-attachments/assets/b9d685dc-430a-4964-94c7-8129a73a08dd" />
