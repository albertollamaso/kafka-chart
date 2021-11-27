# helm chart registry

Commit changes to main branch via PR and git actions will add a new Helm chart to this registry.

charts are at `charts` directory withing this repo.

```
Kafka Helm chart:

charts/kafka
```

charts url (github page): https://albertollamaso.github.io/kafka-chart/

Then you can use this Helm with argo like this

```
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: kafka-app
  namespace: argocd
spec:
  destination:
    namespace: test-helm-argocd
    server: https://kubernetes.default.svc
  project: default
  source:
    chart: kafka
    repoURL: https://albertollamaso.github.io/kafka-chart
    targetRevision: 14.4.1
    helm:
      releaseName: kafka-app-1
  syncPolicy:
    automated:
      prune: true
      selfHeal: true
    syncOptions:
    - CreateNamespace=true
```
