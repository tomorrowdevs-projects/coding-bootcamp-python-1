Il problema parte da un'attività di data cleaning di un file excel contenente migliaia di domande di un test e relative *5 risposte* (`A, B, C, D, E`) di cui *solo 1 è giusta*. 
Semplifichiamo ad 1 sola domanda.

Abbiamo chiesto ad un collega di mettere 1 colonna per ogni risposta, tipo:
``` RISP_A | RISP_B | RISP_C | RISP_D | RISP_E```
ed abbiamo chiesto di aggiungere un colonna contenente quale fosse la risposta corretta, esempio:

Domanda: *Quale famoso matematico inglese collaborò nella Seconda Guerra mondiale con l'esercito britannico per decifrare i codici nazisti?*

```
K       |    L     |    M   |    N   |      O     |       P
-----------------------------------------------------------------
RISP_A  | RISP_B   | RISP_C | RISP_D | RISP_E     | RISP_CORRETTA
Russell | Jeffreys | Turing | Hardy  | Littlewood | C
```

Ovviamente non ci ha ascoltato ed ha fatto così, mettendo sempre la risposta corretta alla colonna `K`:

```
    K         |    L    |    M   |      N     |    O
--------------------------------------------------------
RISP_CORRETTA | RISP_B  | RISP_C | RISP_D     | RISP_E
Turing        | Russell | Hardy  | Littlewood | Jeffreys 
```

Ora, il problema è che dobbiamo inserire i dati all'interno di un database che ha le colonne (ovviamente) come avevamo progettato in precedenza. 
Per le cose che ci dovremo fare dopo e per l'affidabilità dell'inserimento in database, non è funzionante/percorribile la strada di adattare il database al suo file excel.

Quello che dobbiamo fare è *mescolare in modo casuale* tutte le possibili risposte (la giusta e le 4 sbagliate), riposizionarle appunto in modo casuale ma *ricordandoci a quale colonna* ho spostato la *risposta corretta* per poi segnarla nell'apposita colonna aggiuntiva, come volevo io all'inizio.

Lavoriamo ora sul file fatto male che ci ha mandato il nostro amico.
Un primo step nella giusta direzione (se conoscete Excel avete già compreso il perché) è assegnare un numero *da 1 a 5* alle varie colonne/risposte. Tale assegnazione deve essere fatta in modo casuale ricordandovi che *la colonna* (numericamente parlando) *1 conterrà sempre la risposta esatta*.

Nell'esempio sopra, la colonna `K` contiene sempre la risposta corretta e quindi *il numero 1 corrisponderà sempre la risposta giusta*, infatti abbiamo la seguente corrispondenza tra riferimento di colonna alfabetico e numero da 1 a 5:
```   
    K     |    L   |    M   |    N   |    O

    1     |    2   |    3   |    4   |    5
```
Quindi, simulando un rimescolamento, vorrei ottenere nelle colonne successive di excel, qualcosa tipo:
```   
    P   |    Q   |    R   |    S   |    T

    4   |    3   |    1   |    5   |    2
```
L'elaborazine di sopra vuol dire che la mia risposta corretta è la risposta `C` del questionario originale, perché abbiamo spostato la soluzione *Turing* alla posizione `3`.

Aggiungeremo poi altre 5 colonne in cui, tramite formule excel (non è materia di questo esercizio) risaliremo dal numero assegnato (quello da 1 a 5) al testo della risposta da mostrare. Poi, tramite altre formule ricaveremo quale risposta (dopo il rimescolamento) sarà la risposta esatta. 
Nell'esempio sopra, la risposta finale sarà `C`.

Quale approccio logico seguireste?
In cosa potrebbe tornarvi utile Python, come strumento intermedio, per fare cose che Excel non è in grado di fare? *Spoiler: rimescolare i numeri da 1 a 5.*
