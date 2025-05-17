# Specifica l'immagine base. Usiamo una versione Python slim per un'immagine più piccola.
FROM python:3.9-slim

# Imposta le variabili d'ambiente per Python
ENV PYTHONUNBUFFERED 1

# Imposta la directory di lavoro all'interno del container
WORKDIR /app

# Copia il file delle dipendenze (requirements.txt) nella directory di lavoro
# Questo permette a Docker di mettere in cache questo layer se il file non cambia,
# velocizzando le build successive.
COPY requirements.txt .

# Installa le dipendenze specificate in requirements.txt
# --no-cache-dir riduce le dimensioni dell'immagine non salvando i file di cache di pip.
RUN pip install --no-cache-dir -r requirements.txt

# Copia il codice sorgente della tua applicazione nella directory di lavoro.
# Assicurati che la struttura delle directory copiata qui corrisponda a come l'applicazione
# si aspetta di essere trovata (es. 'il_tuo_progetto_flask/' dovrebbe trovarsi dentro '/app/').
COPY sito_flask/ ./sito_flask/

# Esponi la porta su cui il server WSGI (Gunicorn) ascolterà.
# Questa porta sarà accessibile solo all'interno della rete Docker,
# a meno che tu non la mappi esplicitamente in docker-compose.yml o docker run.
# La porta 8000 è una convenzione comune.
EXPOSE 8000

# Definisci il comando che verrà eseguito all'avvio del container.
# Avviamo Gunicorn:
# -w 4: Esegue 4 worker process (un buon punto di partenza, da ottimizzare in base alle risorse)
# -b 0.0.0.0:8000: Fa sì che Gunicorn ascolti su tutte le interfacce sulla porta 8000
# il_tuo_progetto_flask:create_app(): Specifica a Gunicorn dove trovare l'applicazione Flask.
#   - 'il_tuo_progetto_flask': è il nome del modulo/pacchetto Python che contiene la tua app.
#   - 'create_app()': è il nome della variabile o della funzione che restituisce l'istanza dell'applicazione Flask.
#                     Se la tua app è un'istanza chiamata 'app' in un file come 'run.py' nella root del tuo progetto Flask,
#                     il callable potrebbe essere 'run:app'. Se usi il factory pattern come nell'esempio precedente
#                     e la funzione è 'create_app' nel pacchetto 'il_tuo_progetto_flask', il callable è 'il_tuo_progetto_flask:create_app()'.
CMD ["gunicorn", "-w", "4", "-b", "0.0.0.0:8000", "sito_flask:create_app()"]