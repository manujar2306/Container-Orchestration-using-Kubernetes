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

=======================

## Rolling Update and `kubectl set` Commands

This section explains how rolling updates work in Kubernetes and how to update deployments using `kubectl set`.

---

### 🔹 What is Rolling Update?

Rolling Update is a deployment strategy in Kubernetes that updates an application without downtime by gradually replacing old Pods with new ones.

---

### 🔹 Create a Deployment

```bash
kubectl create deployment nginx-deploy --image=nginx
```

---

### 🔹 Update Application (Rolling Update)

Update the container image:

```bash
kubectl set image deployment/nginx-deploy nginx=nginx:1.25

kubectl set image deployment/<deployment-name> <container-name>=<new-image>
```

This triggers a rolling update.

---

### 🔹 Check Rollout Status

```bash
kubectl rollout status deployment/nginx-deploy
```

---

### 🔹 View Rollout History

```bash
kubectl rollout history deployment/nginx-deploy
```

---

### 🔹 Rollback Deployment

```bash
kubectl rollout undo deployment/nginx-deploy
```

---

### 🔹 Rolling Update Strategy (YAML)

```yaml
strategy:
  type: RollingUpdate
  rollingUpdate:
    maxSurge: 1
    maxUnavailable: 1
```

#### Meaning:

* `maxSurge: 1` → One extra Pod can be created during update
* `maxUnavailable: 1` → One Pod can be unavailable during update

---

### 🔹 Other Useful `kubectl set` Commands

#### Set resource limits

```bash
kubectl set resources deployment nginx-deploy --limits=cpu=500m,memory=512Mi
```

#### Set environment variables

```bash
kubectl set env deployment/nginx-deploy ENV=prod
```

---

### 🔹 Full Workflow

```bash
kubectl create deployment nginx-deploy --image=nginx
kubectl set image deployment/nginx-deploy nginx=nginx:1.25
kubectl rollout status deployment/nginx-deploy
kubectl rollout history deployment/nginx-deploy
kubectl rollout undo deployment/nginx-deploy
```

---

### 🔹 Summary

* Rolling updates ensure zero downtime deployment
* `kubectl set image` is used to update applications
* `kubectl rollout` commands help monitor and manage updates

----

