---
title: "Restricted Pod Security Standards"
category: Pod Security
version: 1.8.0
subject: Pod
policyType: "validate"
description: >
    The restricted profile of the Pod Security Standards, which is inclusive of the baseline profile, is a collection of all the most common configurations that can be taken to secure Pods. Beginning with Kyverno 1.8, an entire profile may be assigned to the cluster through a single rule. This policy configures the restricted profile through the latest version of the Pod Security Standards cluster wide.
---

## Policy Definition
<a href="https://github.com/kyverno/policies/raw/main//pod-security/subrule/restricted/restricted-latest/restricted-latest.yaml" target="-blank">/pod-security/subrule/restricted/restricted-latest/restricted-latest.yaml</a>

```yaml
apiVersion: kyverno.io/v1
kind: ClusterPolicy
metadata:
  name: podsecurity-subrule-restricted
  annotations:
    policies.kyverno.io/title: Restricted Pod Security Standards
    policies.kyverno.io/category: Pod Security
    policies.kyverno.io/severity: medium
    kyverno.io/kyverno-version: 1.8.0
    policies.kyverno.io/minversion: 1.8.0
    kyverno.io/kubernetes-version: "1.24"
    policies.kyverno.io/subject: Pod
    policies.kyverno.io/description: >-
      The restricted profile of the Pod Security Standards, which is inclusive of
      the baseline profile, is a collection of all the most common configurations
      that can be taken to secure Pods. Beginning with Kyverno 1.8, an entire profile
      may be assigned to the cluster through a single rule. This policy configures the
      restricted profile through the latest version of the Pod Security Standards cluster wide.
spec:
  background: true
  validationFailureAction: audit
  rules:
  - name: restricted
    match:
      any:
      - resources:
          kinds:
          - Pod
    validate:
      podSecurity:
        level: restricted
        version: latest
```