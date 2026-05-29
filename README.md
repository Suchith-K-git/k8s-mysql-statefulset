# 🚀 MySQL StatefulSet on Kubernetes

This project demonstrates how to deploy MySQL using a StatefulSet in Kubernetes with:

- Namespace
- Headless Service
- StatefulSet
- Persistent Storage
- MySQL Database

---

# 📂 Project Structure

```bash
.
├── namespace.yml
├── service.yml
├── statefulset.yml
└── README.md
```

---

# 📌 What is StatefulSet?

A StatefulSet is used for applications that require:

- Stable Pod Names
- Persistent Storage
- Ordered Deployment
- Ordered Scaling

Perfect for:
- MySQL
- MongoDB
- Kafka
- Redis

Unlike Deployments, StatefulSet pods keep their identity even after restart.

Example:

```bash
mysql-statefulset-0
mysql-statefulset-1
mysql-statefulset-2
```

---

# ⚙️ Step 1: Create Namespace

Apply namespace:

```bash
kubectl apply -f namespace.yml
```

Check namespace:

```bash
kubectl get ns
```

---

# 🌐 Step 2: Create Headless Service

Apply service:

```bash
kubectl apply -f service.yml
```

Check service:

```bash
kubectl get svc -n mysql
```

This Headless Service provides stable DNS for StatefulSet pods.

---

# 🗄️ Step 3: Deploy MySQL StatefulSet

Apply StatefulSet:

```bash
kubectl apply -f statefulset.yml
```

Check StatefulSet:

```bash
kubectl get sts -n mysql
```

---

# 📦 Step 4: Check Pods

```bash
kubectl get pods -n mysql
```

Expected Output:

```bash
NAME                    READY   STATUS    RESTARTS   AGE
mysql-statefulset-0     1/1     Running   0          2m
mysql-statefulset-1     1/1     Running   0          2m
mysql-statefulset-2     1/1     Running   0          2m
```

---

# 💾 Step 5: Check Persistent Volume Claims

```bash
kubectl get pvc -n mysql
```

Expected Output:

```bash
NAME                                 STATUS   VOLUME
mysql-data-mysql-statefulset-0       Bound    pvc-xxxx
mysql-data-mysql-statefulset-1       Bound    pvc-yyyy
mysql-data-mysql-statefulset-2       Bound    pvc-zzzz
```

Each pod gets its own dedicated storage.

---

# 🐚 Step 6: Enter Inside MySQL Pod

```bash
kubectl exec -it mysql-statefulset-0 -n mysql -- bash
```

---

# 🔑 Step 7: Login to MySQL

Inside the container:

```bash
mysql -u root -p
```

Enter password:

```bash
root
```

OR directly:

```bash
mysql -u root -proot
```

---

# 🧪 Step 8: Verify Database

```sql
SHOW DATABASES;
```

Expected Output:

```sql
+--------------------+
| Database           |
+--------------------+
| devops             |
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
```

---

# 🌍 StatefulSet DNS

Each pod gets stable DNS.

Example:

```bash
mysql-statefulset-0.mysql-service.mysql.svc.cluster.local
mysql-statefulset-1.mysql-service.mysql.svc.cluster.local
mysql-statefulset-2.mysql-service.mysql.svc.cluster.local
```

---

# 🛠️ Useful Commands

## Check All Resources

```bash
kubectl get all -n mysql
```

---

## Describe StatefulSet

```bash
kubectl describe sts mysql-statefulset -n mysql
```

---

## Check Logs

```bash
kubectl logs mysql-statefulset-0 -n mysql
```

---

## Scale StatefulSet

```bash
kubectl scale sts mysql-statefulset --replicas=5 -n mysql
```

---

## Delete StatefulSet

```bash
kubectl delete -f statefulset.yml
```

---

## Delete Service

```bash
kubectl delete -f service.yml
```

---

## Delete Namespace

```bash
kubectl delete -f namespace.yml
```

---

# 🎯 Learning Outcome

By completing this project you will understand:

- Kubernetes StatefulSet
- Headless Service
- Persistent Storage
- Persistent Volume Claim (PVC)
- Stable Pod Identity
- MySQL Deployment in Kubernetes

---

# 😂 Fun Fact

Deployment Pods:
> “Who am I today?”

StatefulSet Pods:
> “I am mysql-statefulset-0 and I have responsibilities.” 😎

---

# 👨‍💻 Author

Built with Kubernetes + MySQL + StatefulSet 🚀
