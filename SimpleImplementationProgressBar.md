# progress_bar2.md

Questo script Bash (`progress_bar2.sh`) implementa una **barra di avanzamento visuale (con puntini)** per processi a lunga esecuzione. Dimostra l'uso di processi in background, `trap` per la gestione dei segnali e la sincronizzazione.

---

### Descrizione

Lo script esegue le seguenti azioni:

1.  **Variabili di intervallo**:
    * `interval=1`: Definisce l'intervallo di tempo (in secondi) tra un puntino e l'altro della barra di avanzamento.
    * `long_interval=10`: Definisce la durata simulata del "processo a lunga esecuzione".

2.  **Processo della barra di avanzamento in background**:
    ```bash
    {
        trap "exit" SIGUSR1
        sleep $interval; sleep $interval
        while true
        do
          echo -n '.'
          sleep $interval
        done; } &
    ```
    * Un blocco di comandi `{ ... }` viene eseguito in **background** (`&`). Questo è il processo della barra di avanzamento.
    * `trap "exit" SIGUSR1`: Configura un trap per far sì che questo processo in background termini quando riceve il segnale `SIGUSR1`.
    * `sleep $interval; sleep $interval`: Una piccola pausa iniziale.
    * `while true do echo -n '.'; sleep $interval; done`: Un ciclo infinito che stampa un puntino (`.`) seguito da uno spazio (grazie a `-n`) ogni `interval` secondi, simulando l'avanzamento.

3.  **Cattura del PID e gestione dell'uscita**:
    ```bash
    pid=$!
    trap "echo !; kill -USR1 $pid; wait $pid" EXIT
    ```
    * `pid=$!`: La variabile speciale `$!` cattura il **Process ID (PID)** dell'ultimo comando eseguito in background (cioè il processo della barra di avanzamento).
    * `trap "..." EXIT`: Configura un altro trap che si attiva quando lo script principale sta per uscire (anche in caso di interruzione con `Ctrl+C`). Questo trap assicura che il processo della barra di avanzamento venga terminato correttamente e atteso (`wait $pid`) prima che lo script principale finisca.

4.  **Simulazione del processo principale**:
    ```bash
    echo -n 'Long-running process '
    sleep $long_interval
    echo ' Finished!'
    ```
    * Viene stampato un messaggio e poi lo script "dorme" per `long_interval` secondi, simulando un'operazione che richiede tempo.

5.  **Terminazione della barra di avanzamento**:
    ```bash
    kill -USR1 $pid
    wait $pid
    trap EXIT
    ```
    * `kill -USR1 $pid`: Invia il segnale `SIGUSR1` al processo della barra di avanzamento (usando il PID salvato). Questo attiva il `trap` configurato nel processo della barra, facendolo terminare.
    * `wait $pid`: Attende che il processo della barra di avanzamento sia effettivamente terminato prima di proseguire.
    * `trap EXIT`: Resetta il trap `EXIT` per evitare che venga attivato due volte o interferisca con l'uscita finale.

6.  **Uscita finale**:
    ```bash
    exit $?
    ```
    Lo script termina con il codice di uscita dell'ultimo comando eseguito.

---

### Utilizzo

1.  Salva il codice in un file, ad esempio `progress_bar2.sh`.
2.  Rendilo eseguibile: `chmod +x progress_bar2.sh`.
3.  Eseguilo nel tuo terminale:
    ```bash
    bash ./progress_bar2.sh
    ```
    Vedrai la riga "Long-running process " seguita da una serie di puntini. Dopo 10 secondi, apparirà " Finished!". Puoi provare a interromperlo con `Ctrl+C` per vedere il trap in azione.

---

### Note

* **Requisito Bash**: Come indicato nel commento originale, questo script è stato testato e funziona correttamente con **Bash** e potrebbe non essere compatibile con `sh` (che potrebbe essere un symlink a `dash` su alcune distribuzioni, con funzionalità più limitate).
* **Segnali (`trap`)**: L'uso di `trap` è cruciale qui per gestire in modo pulito l'avvio e la terminazione del processo in background, specialmente in caso di interruzione da parte dell'utente.
* **Processi in background**: L'operatore `&` è fondamentale per permettere alla barra di avanzamento di essere eseguita contemporaneamente al processo principale.