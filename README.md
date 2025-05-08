# Kubernetes Example Voting App

This project is a Kubernetes-based deployment of the [Docker Example Voting App](https://github.com/dockersamples/example-voting-app). It consists of multiple microservices:

- **vote**: Frontend app to cast votes (Node.js)
- **result**: Frontend app to display voting results (Python)
- **worker**: Backend processor to read votes from Redis and write to PostgreSQL (Python)
- **redis**: In-memory data store to queue votes
- **db (PostgreSQL)**: Database to store the vote counts

---

## 📁 Project Structure

| File | Purpose |
|------|---------|
| `vote-deployment.yaml` | Deploys the voting frontend |
| `vote-service.yaml`    | Exposes the voting app on NodePort 31000 |
| `result-deployment.yaml` | Deploys the results frontend |
| `result-service.yaml`    | Exposes the result app on NodePort 31001 |
| `worker-deployment.yaml` | Deploys the background worker |
| `redis-deployment.yaml`  | Deploys Redis |
| `redis-service.yaml`     | ClusterIP service for Redis |
| `db-deployment.yaml`     | Deploys PostgreSQL |
| `db-service.yaml`        | ClusterIP service for PostgreSQL |

---

## 🚀 How to Deploy

Make sure your Kubernetes cluster is running and `kubectl` is configured properly.

```bash
kubectl apply -f db-deployment.yaml
kubectl apply -f db-service.yaml

kubectl apply -f redis-deployment.yaml
kubectl apply -f redis-service.yaml

kubectl apply -f vote-deployment.yaml
kubectl apply -f vote-service.yaml

kubectl apply -f result-deployment.yaml
kubectl apply -f result-service.yaml

kubectl apply -f worker-deployment.yaml
```

---

## 🌐 Accessing the App

- Vote App: `http://<NodeIP>:31000`
- Result App: `http://<NodeIP>:31001`

Replace `<NodeIP>` with the IP of your Kubernetes node (e.g., from `minikube ip`).

---

## 🧹 Clean Up

To delete everything:

```bash
kubectl delete -f .
```

---

## 📝 Notes

- PostgreSQL and Redis are using `emptyDir`, so all data will be lost when pods are deleted.
- You can expose the result app or vote app via Ingress if needed for production environments.
