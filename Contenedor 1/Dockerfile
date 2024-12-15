# Usar la imagen base de Ubuntu
FROM ubuntu:latest

# Damos información sobre la imagen que estamos creando
LABEL \
	authors="DEAW-jesuruiz" \
	version="1.0" \
	description="Tarea evaluativa 1 de UD 3" \
	creationDate="15-12-2024"

# Instalar ProFTPD y otras herramientas necesarias
RUN apt-get update && \
    apt-get install -y proftpd 

# Crear la estructura de directorios para el FTP
RUN mkdir -p /srv/ftp/

# Copiar los archivos locales y de configuración a la carpeta del contenedor
COPY Contenedor1/proftpd.conf /etc/proftpd/
COPY Contenedor1/recursos/* /srv/ftp/

# Exponer los puertos necesarios
EXPOSE 21
EXPOSE 50000-50030

# Comando para iniciar el servidor ProFTPD
CMD ["proftpd", "-n"]