# Usa la imagen oficial de Jenkins que prefieras como base
FROM jenkins/jenkins:lts

# Cambia al usuario root para instalar paquetes
USER root

# Argumento para el GID del grupo docker del host (lo mantenemos por si acaso, aunque no parece ser el factor decisivo ahora)
ARG DOCKER_HOST_GID=1001

# Crea el grupo con el GID del host y añade jenkins a él
RUN groupadd -g ${DOCKER_HOST_GID} docker_host_socket_access || true && \
    usermod -aG docker_host_socket_access jenkins

# Añadir jenkins al grupo 'root' (GID 0) DENTRO del contenedor.
# El grupo 'root' ya debería existir con GID 0.
RUN usermod -aG root jenkins # <--- NUEVA LÍNEA

# Instala dependencias y Docker CLI
RUN apt-get update && \
    apt-get install -y apt-transport-https ca-certificates curl gnupg lsb-release software-properties-common && \
    mkdir -p /etc/apt/keyrings && \
    curl -fsSL https://download.docker.com/linux/debian/gpg | gpg --dearmor -o /etc/apt/keyrings/docker.gpg && \
    echo \
      "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
      $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null && \
    apt-get update && \
    apt-get install -y docker-ce-cli

# Instala Docker Compose (versión standalone V1)
ARG DOCKER_COMPOSE_VERSION=1.29.2
RUN curl -L "https://github.com/docker/compose/releases/download/${DOCKER_COMPOSE_VERSION}/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose && \
    chmod +x /usr/local/bin/docker-compose

# Vuelve al usuario jenkins
USER jenkins