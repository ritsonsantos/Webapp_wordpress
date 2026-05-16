
# Laboratório



Para rodar o projeto você precisa dos seguintes componentes:

- Docker
- Kubectl

Este é um laboratório feito no kubernetes com os seguintes serviços:

- WordPress
- MySQL
- Kubernetes
- Configmap 
- Secret
- PersistVolume
- Service

## Deployment

- Criar namespace

```bash
  kubectl create namespace devops-lab
```

- Criar Secret

```bash
  kubectl create secret generic mysql-secret \
--from-literal=MYSQL_ROOT_PASSWORD=root123 \
--from-literal=MYSQL_DATABASE=wordpress \
--from-literal=MYSQL_USER=wpuser \
--from-literal=MYSQL_PASSWORD=wppass \
-n devops-lab
```
- Criar MySQL com Volume usando yaml

```bash
kubectl apply -f mysql.yaml
```

- Expose do serviço MySQL

```bash
  kubectl expose deployment mysql \
--port=3306 \
--type=ClusterIP \
-n devops-lab
```

- Criar o WordPress com yaml

```bash
kubectl apply -f wordpress.yaml
```

- Expose do serviço WordPress

```bash
kubectl expose deployment wordpress \
--port=80 \
--type=NodePort \
-n devops-lab
```

- Ver a porta

```bash
  kubectl get svc -n devops-lab
```

- Acessar pelo navegador

```bash
  http://IP_DO_NODE:PORTA
```
