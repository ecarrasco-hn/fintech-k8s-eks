# FinTech Kubernetes Deployment on Amazon EKS

Este repositorio contiene los archivos de configuración utilizados para desplegar una aplicación de gestión financiera sobre un clúster de Kubernetes en Amazon EKS. La solución implementa una arquitectura de tres capas formada por un frontend basado en React y NGINX, un backend desarrollado en Node.js y una base de datos PostgreSQL con almacenamiento persistente mediante Amazon EFS.

## Arquitectura de la solución

La aplicación está compuesta por los siguientes elementos:

* **Frontend**: Aplicación web desarrollada con React y servida mediante NGINX.
* **Backend**: Servicio de negocio desarrollado en Node.js.
* **Base de datos**: PostgreSQL.
* **Persistencia**: Amazon EFS integrado mediante Persistent Volume y Persistent Volume Claim.

## Estructura del repositorio

```text
fintech-k8s-eks
│
├── namespace.yaml
│
├── postgres
│   ├── postgres-secret.yaml
│   ├── postgres-pv.yaml
│   ├── postgres-pvc.yaml
│   ├── postgres-deployment.yaml
│   └── postgres-service.yaml
│
├── backend
│   ├── backend-configmap.yaml
│   ├── backend-deployment.yaml
│   └── backend-service.yaml
│
└── frontend
    ├── frontend-nginx-configmap.yaml
    ├── frontend-deployment.yaml
    └── frontend-service.yaml
```

## Prerrequisitos

Antes de desplegar la solución es necesario disponer de:

* Un clúster Amazon EKS operativo.
* Dos nodos de trabajo.
* Amazon EFS previamente creado.
* Amazon EFS CSI Driver instalado en el clúster.
* `kubectl` configurado con acceso al clúster.

## Orden recomendado de despliegue

### 1. Crear el namespace

```bash
kubectl apply -f namespace.yaml
```

### 2. Desplegar PostgreSQL

```bash
kubectl apply -f postgres/postgres-secret.yaml
kubectl apply -f postgres/postgres-pv.yaml
kubectl apply -f postgres/postgres-pvc.yaml
kubectl apply -f postgres/postgres-deployment.yaml
kubectl apply -f postgres/postgres-service.yaml
```

### 3. Desplegar el Backend

```bash
kubectl apply -f backend/backend-configmap.yaml
kubectl apply -f backend/backend-deployment.yaml
kubectl apply -f backend/backend-service.yaml
```

### 4. Desplegar el Frontend

```bash
kubectl apply -f frontend/frontend-nginx-configmap.yaml
kubectl apply -f frontend/frontend-deployment.yaml
kubectl apply -f frontend/frontend-service.yaml
```

## Verificación

Consultar el estado de los recursos:

```bash
kubectl get all -n fintech
```

Verificar el almacenamiento persistente:

```bash
kubectl get pv
kubectl get pvc -n fintech
```

Verificar los servicios:

```bash
kubectl get svc -n fintech
```

## Flujo de la aplicación

```text
Usuarios
    │
Load Balancer
    │
Frontend (React + NGINX)
    │
Backend (Node.js)
    │
PostgreSQL
    │
Amazon EFS
```

## Tecnologías utilizadas

* Amazon EKS
* Kubernetes
* Amazon EFS
* React
* NGINX
* Node.js
* PostgreSQL
* Docker

## Autor

**Elvin Carrasco**

Máster Universitario en Desarrollo y Operaciones (DevOps)

Universidad Internacional de La Rioja (UNIR)
