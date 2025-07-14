# naked_variables.md

Questo script Bash (`naked_variables.sh`) illustra le circostanze in cui una **variabile viene utilizzata senza il prefisso dollaro (`$`)**, ovvero quando le si sta **assegnando un valore** piuttosto che facendovi riferimento.

---

### Descrizione

Lo script dimostra vari scenari di assegnazione di variabili:

1.  **Assegnazione Diretta**:
    ```bash
    a=879
    echo "The value of \"a\" is $a."
    ```
    Qui, `a` è "nuda" quando le viene assegnato il valore `879`. Per farvi riferimento (cioè per recuperare il suo valore), si usa `$a`.

2.  **Assegnazione con `let`**:
    ```bash
    let a=16+5
    echo "The value of \"a\" is now $a."
    ```
    Il comando `let` esegue un'operazione aritmetica e assegna il risultato. Anche qui, `a` è senza `$` al momento dell'assegnazione.

3.  **In un ciclo `for`**:
    ```bash
    for a in 7 8 9 11
    do
      echo -n "$a "
    done
    ```
    Nel ciclo `for`, la variabile `a` assume sequenzialmente i valori `7`, `8`, `9`, `11`. Durante ogni iterazione, quando `a` riceve il nuovo valore, è in modalità di assegnazione (senza `$`). Quando stampata, `echo -n "$a "`, viene referenziata con `$`.

4.  **In un'istruzione `read`**:
    ```bash
    echo -n "Enter \"a\" "
    read a
    echo "The value of \"a\" is now $a."
    ```
    Il comando `read` legge l'input dell'utente dalla console e lo assegna alla variabile specificata. Quando si usa `read a`, la variabile `a` è senza `$`, poiché le si sta assegnando il valore digitato dall'utente.

---

### Utilizzo

1.  Salva il codice in un file, ad esempio `naked_variables.sh`.
2.  Rendilo eseguibile: `chmod +x naked_variables.sh`.
3.  Eseguilo nel tuo terminale:
    ```bash
    ./naked_variables.sh
    ```
    Durante l'esecuzione, lo script ti chiederà di inserire un valore per `a`.

---

### Note

* La regola generale in Bash è:
    * Quando si **assegna** o si **modifica** il valore di una variabile, si usa il suo nome **senza il prefisso `$`.**
    * Quando si **recupera** o si **referenzia** il valore di una variabile, si usa il suo nome **con il prefisso `$`.**
* Questa distinzione è fondamentale per comprendere come manipolare le variabili negli script Bash.