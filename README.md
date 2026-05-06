# Container-Orchestration-using-Kubernetes
Explanation for deployment yaml - rolling update

During Rolling Update
Step 1:
Current pods = 3
Kubernetes creates +1 new pod (because maxSurge: 1)

-> Total pods = 4

Step 2:
Kubernetes deletes 1 old pod (because maxUnavailable: 1)

-> Total pods = 3 again

Step 3:
Repeat until all pods are update
