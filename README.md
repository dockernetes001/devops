# Pipeline DevOps para Proyecto Vue con Jenkins y Nginx

Este proyecto incluye:

- **Jenkins** con Node.js, Yarn y Cypress configurado para pruebas headless.
- **Dos servidores Nginx + SSH** para desplegar los builds de Vue.
- Pipeline CI/CD que compila Vue, ejecuta tests y despliega automáticamente vía SSH.

## 1️⃣ Estructura del proyecto

├── jenkins/ # Dockerfile de Jenkins con Node.js y Cypress
├── servidor_nginx/ # Dockerfile de Nginx + SSH
├── proyecto1/ # Código Vue para despliegue en web1
├── proyecto2/ # Código Vue para despliegue en web2
└── docker-compose.yml

## 2️⃣ Levantar los contenedores

1. Construir y levantar todos los servicios:
    
```bash
docker-compose up -d --build
```

## 3️⃣ Configurar llaves SSH para Jenkins

1. Generar una llave SSH en el contenedor de Jenkins:

```bash
docker exec -it jenkins-vue /bin/bash
ssh-keygen -t rsa -b 4096 -C "jenkins
```

2. Copiar la llave pública al servidor remoto (Nginx):

```bash
ssh-copy-id -i /var/jenkins_home/.ssh/id_rsa.pub user@vue-nginx-1
ssh-copy-id -i /var/jenkins_home/.ssh/id_rsa.pub user@vue-nginx-2
```

3. Probar la conexión SSH:

```bash
ssh user@vue-nginx-1 "echo Conexión OK"
ssh user@vue-nginx-2 "echo Conexión OK"
```

4. Agregar las llaves SSH a los hosts conocidos:

```bash
ssh-keyscan -H vue-nginx-1 >> ~/.ssh/known_hosts
ssh-keyscan -H vue-nginx-2 >> ~/.ssh/known_hosts
```
