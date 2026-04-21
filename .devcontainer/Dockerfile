# Usamos la imagen base de Ubuntu oficial de Microsoft
FROM mcr.microsoft.com/devcontainers/base:ubuntu

# Instalamos MariaDB directamente usando el gestor de paquetes de Linux (apt-get)
# Esto salta la necesidad de usar el registro de Features de GitHub
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends mariadb-server \
    && apt-get clean && rm -rf /var/lib/apt/lists/*