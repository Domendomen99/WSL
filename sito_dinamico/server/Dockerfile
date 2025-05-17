# Specifica l'immagine base ufficiale di Apache HTTP Server
FROM httpd:2.4

# Copia il file di configurazione personalizzato di Apache per il Virtual Host
# Lo copiamo in una directory comune per i file di configurazione extra.
# Il nome del file è arbitrario, ma '.conf' è una convenzione.
COPY server/apache.conf /usr/local/apache2/conf/extra/httpd-vhosts.conf

# Abilita i moduli proxy necessari in Apache.
# Le immagini ufficiali httpd spesso includono già questi moduli,
# ma potrebbero non essere abilitati di default a seconda della versione/configurazione.
# Se usi una distro-based image (es. ubuntu + apache2), potresti usare RUN a2enmod proxy proxy_http.
# Con l'immagine ufficiale, spesso è sufficiente la configurazione nel file .conf.
# Se necessario, potresti aggiungere qui comandi RUN per abilitare moduli specifici.
# Esempio (sintassi specifica dell'immagine base):
# RUN sed -i '/#LoadModule proxy_module/s/^#//' /usr/local/apache2/conf/httpd.conf && \
#     sed -i '/#LoadModule proxy_http_module/s/^#//' /usr/local/apache2/conf/httpd.conf

# Assicurati che il file httpd-vhosts.conf sia incluso nella configurazione principale di Apache.
# L'immagine ufficiale httpd non include di default i file dalla directory extra.
# Aggiungiamo quindi una riga di Include nel file di configurazione principale.
RUN echo "Include conf/extra/httpd-vhosts.conf" >> /usr/local/apache2/conf/httpd.conf

# Esponi le porte standard HTTP e HTTPS (se prevedi di gestire HTTPS qui)
# Queste sono le porte a cui il mondo esterno si connetterà per raggiungere il tuo sito.
EXPOSE 80
# EXPOSE 443 # Decommenta se gestisci HTTPS in questo container

# Il comando di avvio di Apache è già definito nell'immagine base (CMD ["httpd-foreground"]).
# Non è necessario definirlo nuovamente a meno di esigenze particolari.