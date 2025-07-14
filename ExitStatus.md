# exit_status.md

Questo script Bash (`exit_status.sh`) dimostra il concetto di **codice di uscita (exit status)** nei comandi e negli script Bash, che indica il successo o il fallimento di un'operazione.

---

### Descrizione

Lo script illustra come funziona il codice di uscita (`$?`) attraverso questi passaggi:

1.  **Comando riuscito**:
    ```bash
    echo hello
    echo $?
    ```
    Esegue un semplice comando `echo` (che stampa "hello"). Poiché `echo` viene eseguito con successo, il valore di `$?` (il codice di uscita del comando precedente) sarà `0`. Per convenzione, `0` indica il **successo**.

2.  **Comando fallito**:
    ```bash
    lskdf      # Unrecognized command.
    echo $?
    ```
    Tenta di eseguire un comando inesistente (`lskdf`). Questo fallisce. Di conseguenza, il valore di `$?` sarà un numero **diverso da zero** (specifico del tipo di errore, ad esempio `127` per "comando non trovato"), indicando un **fallimento** o una condizione anomala.

3.  **Uscita esplicita dello script**:
    ```bash
    exit 113
    ```
    Lo script termina esplicitamente con `exit 113`. Questo significa che quando lo script termina, il suo codice di uscita (che puoi verificare digitando `echo $?` nel terminale dopo l'esecuzione dello script) sarà `113`. Qualsiasi codice che segue `exit` non verrà eseguito.

---

### Utilizzo

1.  Salva il codice in un file, ad esempio `exit_status.sh`.
2.  Rendilo eseguibile: `chmod +x exit_status.sh`.
3.  Eseguilo nel tuo terminale:
    ```bash
    ./exit_status.sh
    ```
4.  Dopo l'esecuzione, digita `echo $?` per vedere il codice di uscita dello script, che sarà `113`.

---

### Note

* **Convenzione**: Un codice di uscita di `0` significa che il comando o lo script è stato eseguito **senza errori**. Qualsiasi valore **diverso da zero** indica un qualche tipo di **errore** o un'eccezione.
* **Debug e logica condizionale**: Il codice di uscita è fondamentale negli script Bash per la programmazione condizionale (es. con `if` statement) e per il debug, permettendo agli script di reagire in base al successo o al fallimento dei comandi eseguiti.