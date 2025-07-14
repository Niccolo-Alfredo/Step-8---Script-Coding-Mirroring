# script_parameters.md

Questo script Bash (`script_parameters.sh`) dimostra come accedere e gestire i **parametri passati da riga di comando** a uno script. Richiede un numero minimo di parametri per essere eseguito correttamente.

---

### Descrizione

Lo script esegue le seguenti operazioni:

1.  **Definizione del numero minimo di parametri**:
    * `MINPARAMS=10`: Imposta una variabile che definisce il numero minimo di argomenti che lo script si aspetta.

2.  **Nome dello script**:
    * `echo "The name of this script is \"$0\"."`: Stampa il nome dello script inclusivo del percorso relativo o assoluto con cui è stato chiamato (es. `./script_parameters.sh`).
    * `echo "The name of this script is \"\`basename $0\`\"."`: Stampa solo il nome del file dello script, rimuovendo qualsiasi informazione di percorso (`basename`).

3.  **Accesso ai singoli parametri**:
    * Vengono mostrati esempi su come accedere ai primi tre parametri (`$1`, `$2`, `$3`).
    * **Importante**: Per i parametri oltre il nono (cioè dal decimo in poi), è necessario racchiudere il numero tra parentesi graffe, come in `${10}`. Questo è dimostrato per il decimo parametro.
    * `if [ -n "$1" ]`: Questo controllo verifica se il parametro esiste (non è vuoto).

4.  **Stampa di tutti i parametri**:
    * `echo "All the command-line parameters are: "$*""`: Stampa tutti i parametri passati allo script come un'unica stringa.

5.  **Verifica del numero minimo di parametri**:
    * `if [ $# -lt "$MINPARAMS" ]`: `$#` è una variabile speciale in Bash che contiene il numero totale di parametri passati allo script. Questo `if` confronta `$#` con `MINPARAMS`.
    * Se il numero di parametri è inferiore a `MINPARAMS`, lo script stampa un avviso.

6.  **Uscita**:
    * `exit 0`: Termina lo script con un codice di successo.

---

### Utilizzo

1.  Salva il codice in un file, ad esempio `script_parameters.sh`.
2.  Rendilo eseguibile: `chmod +x script_parameters.sh`.
3.  Eseguilo passando almeno 10 parametri, ad esempio:
    ```bash
    ./script_parameters.sh uno due tre quattro cinque sei sette otto nove dieci undici
    ```
    Lo script visualizzerà il nome, i primi parametri e un riepilogo di tutti gli argomenti. Se lo esegui con meno di 10 parametri, ti avviserà.

---

### Note

* **Variabili speciali**: `$0`, `$#`, `$*` sono esempi di variabili speciali in Bash che forniscono informazioni sugli argomenti della riga di comando e sul nome dello script.
* **Quoting**: L'uso delle virgolette (`" "`) attorno alle variabili (`"$1"`, `"$*"`) è una buona pratica per evitare problemi con spazi o caratteri speciali all'interno dei parametri.