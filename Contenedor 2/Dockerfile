# Usamos la última imagen base de Ubuntu
FROM ubuntu:latest

# Damos información sobre la imagen que estamos creando
LABEL \
	authors="DEAW-jesuruiz" \
	version="1.0" \
	description="Tarea evaluativa 1 de UD 3" \
	creationDate="15-12-2024"

# Instalamos ProFTPD y otras utilidades necesarias 
RUN apt-get update && \ 
    apt-get install -y proftpd proftpd-mod-crypto openssl nano 

# Creamos el usuario "deaw" con contraseña "deaw" y su carpeta 
RUN useradd -m -d /srv/deaw -s /usr/sbin/nologin deaw && \
    echo "deaw:deaw" | chpasswd && \ 
    mkdir -p /srv/deaw && \ 
    chown -R deaw:deaw /srv/deaw

# Copiamos los archivos locales a la carpeta del contenedor
COPY Contenedor2/recursos/* /srv/deaw/

# Creamos el certificado autofirmado y guardamos en las carpetas de certificados 
RUN openssl req -newkey rsa:4096 -days 365 -nodes -x509 \ 
    -subj "/CN=Jesus Angel Ruiz" \ 
    -keyout /etc/ssl/private/deaw.key \ 
    -out /etc/ssl/certs/deaw.pem

# Copiamos los archivos locales y de configuración a la carpeta del contenedor
COPY Contenedor2/proftpd.conf /etc/proftpd/
COPY Contenedor2/tls.conf /etc/proftpd/
COPY Contenedor2/modules.conf /etc/proftpd/

# Exponemos los puertos necesarios
EXPOSE 21
EXPOSE 50000-50030

# Ejecutamos el comando para iniciar el servidor ProFTPD
CMD ["proftpd", "-n"]