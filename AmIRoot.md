# am-i-root.md

Questo script Bash (`am-i-root.sh`) verifica se l'utente che lo sta eseguendo ha i privilegi di **root**.

---

### Descrizione

Lo script utilizza due metodi per determinare se l'utente è root:

1.  **Controllo dell'UID**:
    * Definisce `ROOT_UID` come `0`, che è l'ID utente (UID) riservato all'utente root sui sistemi Unix/Linux.
    * Verifica se il `$UID` dell'utente corrente (una variabile di sistema Bash che contiene l'UID dell'utente che esegue lo script) è uguale a `ROOT_UID`.
    * Stampa un messaggio appropriato (`"You are root."` o `"You are just an ordinary user..."`).

2.  **Controllo del nome utente (metodo alternativo, non eseguito)**:
    * Questa sezione di codice è commentata dal `#` e non viene eseguita a causa del comando `exit 0` precedente.
    * Definisce `ROOTUSER_NAME` come `"root"`.
    * Usa `id -nu` (o `whoami`) per ottenere il nome utente dell'esecutore.
    * Confronta il nome utente ottenuto con `ROOTUSER_NAME` e stampa un messaggio.

---

### Utilizzo

1.  Salva il codice in un file, ad esempio `am-i-root.sh`.
2.  Rendilo eseguibile: `chmod +x am-i-root.sh`.
3.  Eseguilo da qualsiasi utente: `./am-i-root.sh`.

---

### Note

* **`$UID` vs. `id -nu` / `whoami`**: Il controllo tramite `$UID` è il metodo più robusto e consigliato in Bash per verificare i privilegi di root, poiché si basa sull'ID numerico univoco e non sul nome (che potrebbe essere modificato o duplicato in configurazioni particolari, anche se raro per "root").
* **Terminazione precoce**: Il comando `exit 0` fa terminare lo script immediatamente. Qualsiasi codice che segue `exit` non verrà eseguito.