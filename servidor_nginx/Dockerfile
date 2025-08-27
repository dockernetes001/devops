# Imagen base
FROM ubuntu:20.04

# Evitar interacciones en la instalación
ENV DEBIAN_FRONTEND=noninteractive

# Actualizar e instalar nginx y ssh
RUN apt-get update && apt-get install -y \
    nginx \
    openssh-server \
    && apt-get clean

# Crear usuario para acceso SSH
RUN useradd -m -s /bin/bash user && echo "user:pass" | chpasswd

# Configuración de SSH
RUN mkdir /var/run/sshd

# Exponer puertos (80 para nginx y 22 para ssh)
EXPOSE 80 22

# Levantar ambos servicios en paralelo
CMD service ssh start && nginx -g 'daemon off;'
