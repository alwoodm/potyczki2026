W Addmission Control dodajemy nową pozycje
<img width="1917" height="930" alt="obraz" src="https://github.com/user-attachments/assets/74313963-0d4f-4577-8e6f-d82fe4b3343f" />
W wcześniej wymienianej opcji import yaml dodajemy. MariaDB dostępna tylko dla podow strony internetowaej
```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-only-krzak-pol-web
  namespace: klienci-premium
spec:
  podSelector: {}
  policyTypes:
    - Ingress
  ingress:
    - from:
        - namespaceSelector:
            matchLabels:
              kubernetes.io/metadata.name: krzak-pol-web
```
