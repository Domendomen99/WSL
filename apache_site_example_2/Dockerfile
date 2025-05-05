FROM debian:bullseye

# Evita domande interattive durante l'installazione
ENV DEBIAN_FRONTEND=noninteractive

# Installa Apache
RUN apt update && \
    apt install -y apache2 && \
    apt clean && \
    rm -rf /var/lib/apt/lists/*

# Copia il file HTML nella root del sito
COPY public/ /var/www/html/

# Espone la porta 80
EXPOSE 80

# Comando di avvio
CMD ["apachectl", "-D", "FOREGROUND"]

