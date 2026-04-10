Dodanie label tier: zloto w Node klusterteam
<img width="1919" height="943" alt="obraz" src="https://github.com/user-attachments/assets/dbadeda7-9b14-4d90-9c3e-79bbcb55f813" />
Dodanie reguły do mariaDB wymuszającej uruchamiania podów wyłącznie na węzłach spełniających określone kryteria labelowe
```yaml
securityContext: {}
      affinity:
        nodeAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
            nodeSelectorTerms:
              - matchExpressions:
                  - key: tier
                    operator: In
                    values:
                      - zloto
      terminationGracePeriodSeconds: 30
```
Import yaml. yaml wymusza dostępność minimum 4 replik podczas operacji administracyjnych (drain, upgrade). Przy 5 replikach maksymalnie 1 pod może być jednocześnie niedostępny.
<img width="1919" height="947" alt="obraz" src="https://github.com/user-attachments/assets/518317d4-01ee-45b8-aeec-a15b9cef6809" />
