# cleanup_logs.md

Questo script Bash pulisce i file di log di sistema `messages` e `wtmp`, azzerandone il contenuto. Utile per liberare spazio su disco.

---

### Descrizione

1.  **`cd /var/log`**: Naviga nella directory standard dei file di log.
2.  **`cat /dev/null > messages`**: Svuota il contenuto del file `messages` (log di sistema generali).
3.  **`cat /dev/null > wtmp`**: Svuota il contenuto del file `wtmp` (registra accessi/disconnessioni utenti, reboot).
4.  **`echo "Log files cleaned up."`**: Messaggio di conferma.

---

### Utilizzo

1.  Salva come `cleanup.sh`.
2.  Rendilo eseguibile: `chmod +x cleanup.sh`.
3.  Esegui **come utente root**: `sudo ./cleanup.sh`.

---

### Avvertenze

* **Necessita di `root`**: I file di log sono protetti e richiedono privilegi elevati.
* **Perdita di dati**: Il contenuto dei log viene **definitivamente cancellato**. Non recuperabile.
* **Alternative**: In produzione, considera `logrotate` per una gestione automatica e sicura dei log.

---