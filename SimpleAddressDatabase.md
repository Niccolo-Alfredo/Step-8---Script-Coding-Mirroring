# fetch_address.md

Questo script Bash (`fetch_address.sh`) illustra l'uso delle **array associative** (`declare -A`) per memorizzare e recuperare dati utilizzando chiavi stringa, simili a dizionari o hash map in altri linguaggi di programmazione.

---

### Descrizione

Lo script esegue le seguenti operazioni:

1.  **Dichiarazione dell'array associativo**:
    ```bash
    declare -A address
    ```
    La riga `declare -A address` dichiara una variabile chiamata `address` come un'array associativa. Questo permette di usare stringhe (nomi) come indici per accedere ai valori, anziché solo numeri interi.

2.  **Assegnazione dei valori**:
    ```bash
    address[Charles]="414 W. 10th Ave., Baltimore, MD 21236"
    address[John]="202 E. 3rd St., New York, NY 10009"
    address[Wilma]="1854 Vermont Ave, Los Angeles, CA 90023"
    ```
    Vengono assegnati indirizzi a chiavi come "Charles", "John" e "Wilma". Ogni chiave è racchiusa tra parentesi quadre.

3.  **Accesso e stampa dei valori**:
    ```bash
    echo "Charles's address is ${address[Charles]}."
    echo "Wilma's address is ${address[Wilma]}."
    echo "John's address is ${address[John]}."
    ```
    I valori associati a specifiche chiavi vengono recuperati e stampati. La sintassi `${array_name[key]}` viene usata per accedere al valore.

4.  **Stampa delle chiavi (indici)**:
    ```bash
    echo "${!address[*]}"
    ```
    Questa riga speciale stampa **tutte le chiavi** (o indici) definite nell'array associativo. L'uso di `!` prima del nome dell'array e `[*]` indica che si vogliono elencare le chiavi anziché i valori.

---

### Utilizzo

1.  Salva il codice in un file, ad esempio `fetch_address.sh`.
2.  Rendilo eseguibile: `chmod +x fetch_address.sh`.
3.  Eseguilo nel tuo terminale:
    ```bash
    ./fetch_address.sh
    ```

---

### Note

* **Bash 4+**: Le array associative sono una funzionalità introdotta in **Bash versione 4.0 e successive**. Questo script non funzionerà con versioni precedenti di Bash (es. Bash 3.x). Puoi controllare la tua versione di Bash con `bash --version`.
* **Flessibilità**: Le array associative sono estremamente utili per memorizzare dati correlati in cui le informazioni sono accessibili tramite un nome descrittivo (la chiave) anziché un indice numerico.