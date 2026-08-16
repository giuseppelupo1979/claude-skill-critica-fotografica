# Critica fotografica per ChatGPT

Un protocollo di istruzioni per un GPT personalizzato in ChatGPT, che produce su una fotografia una lettura critica strutturata: tecnica, geometrica, compositiva, narrativa, artistica e poetica. Con riferimenti motivati ai fotografi del Novecento, un piano di post produzione operativo e indicazioni concrete per lo scatto successivo.

Non è un generatore di complimenti, non è un ripasso della regola dei terzi, non è una lista di cursori da spostare. È una diagnosi ancorata a ciò che si vede davvero nell'immagine, che distingue quello che osserva da quello che deduce, e che dichiara esplicitamente quando il dato non c'è.

---

## Indice

- [Cosa fa](#cosa-fa)
- [Perché esiste](#perché-esiste)
- [Installazione](#installazione)
- [Uso](#uso)
- [Le cinque modalità](#le-cinque-modalità)
- [Architettura della skill](#architettura-della-skill)
  - [Protocollo epistemico](#protocollo-epistemico)
  - [Pipeline interna obbligatoria](#pipeline-interna-obbligatoria)
  - [Ancoraggio dei giudizi](#ancoraggio-dei-giudizi)
  - [Vincolo anti normalizzazione](#vincolo-anti-normalizzazione)
  - [Divieti anti invenzione](#divieti-anti-invenzione)
- [La scheda completa: tredici sezioni](#la-scheda-completa-tredici-sezioni)
- [Sistema di valutazione](#sistema-di-valutazione)
- [I file di riferimento](#i-file-di-riferimento)
  - [canone.md](#canonemd--il-canone-come-problemi-visivi)
  - [postproduzione.md](#postproduzionemd--strategie-condizionali)
- [Modalità serie e portfolio](#modalità-serie-e-portfolio)
- [Tono e stile](#tono-e-stile)
- [Esempi di calibrazione](#esempi-di-calibrazione)
- [Struttura del repository](#struttura-del-repository)
- [Limiti noti](#limiti-noti)
- [Personalizzare la skill](#personalizzare-la-skill)
- [Criterio di successo](#criterio-di-successo)
- [Licenza](#licenza)

---

## Cosa fa

Carichi una o più fotografie e chiedi un parere. La skill si attiva da sola e restituisce:

- una **lettura a freddo** di cosa colpisce nei primi tre secondi e dove va l'occhio;
- una o più **ipotesi sull'intenzione dell'autore**, ricavate dall'immagine e non dal gusto di chi giudica;
- una **scheda tecnica** su esposizione, fuoco, luce, colore, rumore, con marcatura esplicita di ciò che è stimato e di ciò che non è determinabile;
- un'analisi di **geometria e composizione** che distingue la violazione consapevole delle regole dalla violazione distratta;
- una valutazione di **soggetto, momento ed espressione**, con nota etica quando servono;
- una **lettura artistica e poetica**, dichiaratamente interpretativa, con titolo proposto e un testo di massimo quattro righe;
- una **genealogia visiva**: da due a quattro fotografi del Novecento, citati solo se il riferimento regge davvero;
- una **controanalisi** che tenta di confutare la lettura appena fatta, prima del verdetto;
- una **valutazione numerica** su sette assi, con pesi che cambiano in base al genere e calcolo mostrato;
- un **piano di post produzione operativo**, dove ogni intervento è agganciato a un problema visivo dichiarato;
- indicazioni di **pre scatto** per la prossima volta, azionabili sul campo;
- **la singola priorità**: l'unico intervento che cambierebbe di più l'immagine;
- un **esercizio** pratico e verificabile per la prossima uscita.

## Perché esiste

Una critica fotografica generata da un modello linguistico fallisce quasi sempre negli stessi tre punti, e la skill è costruita per chiudere esattamente quelle tre falle.

**Primo: presenta come osservazione ciò che è deduzione, e come misura ciò che è impressione.** Nasce così la frase "l'istogramma mostra ombre chiuse" scritta davanti a un JPEG compresso da cui nessun istogramma è ricavabile. La risposta è il protocollo epistemico a cinque livelli.

**Secondo: normalizza.** Spinge ogni immagine verso ordine, pulizia, nitidezza, simmetria, orizzonte dritto. Ma una fotografia in chiave Moriyama peggiora se la pulisci, e una in chiave Klein muore se la raddrizzi. La risposta è il vincolo anti normalizzazione.

**Terzo: cita per prestigio.** "Ricorda Cartier-Bresson" applicato a qualunque immagine con una figura che cammina. La risposta è un canone codificato come problemi visivi, dove per ogni autore il campo decisivo non è quando citarlo ma **quando non citarlo**.

L'interlocutore previsto è un fotografo avanzato. La skill dà del tu e tratta da pari.

## Configurazione in ChatGPT

Questa versione è pensata prima di tutto per un **GPT personalizzato in ChatGPT**. ChatGPT non carica automaticamente un file `SKILL.md` da un repository: usa invece le sue **Istruzioni** e i file di **Conoscenza**.

1. Apri [l’editor dei GPT](https://chatgpt.com/gpts/editor) sul web e crea un GPT.
2. Nella scheda **Configura**, incolla nelle **Istruzioni** il contenuto di `critica-fotografica/SKILL.md`, escluso il frontmatter YAML iniziale.
3. Carica come **Conoscenza** `critica-fotografica/references/canone.md` e `critica-fotografica/references/postproduzione.md`.
4. Aggiungi come prompt iniziali alcuni esempi da [examples/USAGE.md](examples/USAGE.md).
5. Salva e prova il GPT allegando una fotografia.

Per una critica puntuale delle immagini abilita la capacità di analisi delle immagini disponibile nel tuo piano. Le funzionalità per creare o modificare GPT dipendono dal piano e dalle autorizzazioni dell’area di lavoro.

### Compatibilità Claude

La stessa struttura rimane compatibile con Claude: copia la cartella `critica-fotografica/` nella directory delle skill prevista dal tuo ambiente Claude.

## Uso

La skill si attiva senza che tu la nomini. Bastano richieste come:

```
che ne pensi di questa foto?
```
```
critica questo scatto
```
```
dammi un voto
```
```
come la ritaglio?
```
```
come la sviluppo in post?
```
```
di queste dodici quali tengo per il portfolio?
```

Puoi anche forzare la modalità:

```
parere rapido su questa
```
```
modalità serie su queste otto immagini
```
```
questa va in stampa fine art, 50x70 su baritata
```

Più contesto dai, più la critica è precisa. Utili in particolare: il genere a cui l'immagine appartiene, il progetto di cui fa parte, la destinazione (web, stampa, mostra, concorso), le dimensioni in pixel del file originale se ti interessa un giudizio sulla dimensione massima di stampa.

## Le cinque modalità

La modalità viene sempre dichiarata in apertura. Se non la specifichi, viene dedotta dal numero di immagini e dal tipo di richiesta, e la deduzione viene esplicitata.

| Modalità | Quando si attiva | Formato dell'output |
|---|---|---|
| `rapida` | chiedi un parere veloce | massimo 300 parole: diagnosi secca, tre interventi, un voto |
| `completa` | predefinita, una sola immagine | scheda integrale a 13 sezioni |
| `serie` | da 3 a 20 immagini, sequenza o progetto | format lock dedicato, non 20 schede complete |
| `portfolio` | selezione da un insieme non narrativo | giudizio per autonomia e rappresentatività |
| `stampa` | l'immagine è destinata alla carta | scheda completa più focus su densità, gamut, dimensione |

## Architettura della skill

Cinque meccanismi tengono in piedi tutto il resto. Sono la parte non negoziabile: se li togli, resta una scheda vuota da riempire con luoghi comuni.

### Protocollo epistemico

Ogni affermazione è classificata su cinque livelli:

| Livello | Significato |
|---|---|
| **OSSERVATO** | direttamente visibile nell'immagine |
| **RICAVATO** | deduzione fortemente sostenuta da ciò che si vede |
| **STIMATO** | valutazione tecnica non misurabile con i dati disponibili |
| **INTERPRETATO** | lettura narrativa, simbolica o artistica |
| **NON DETERMINABILE** | informazione che l'immagine fornita non consente di stabilire |

**Regola di parsimonia.** Marcare ogni frase renderebbe la scheda illeggibile e il rigore diventerebbe rumore. Quindi OSSERVATO è il livello predefinito e non si marca mai; `[STIMATO]` e `[NON DETERMINABILE]` si marcano sempre; `[RICAVATO]` si marca solo quando la deduzione regge un giudizio importante; per le sezioni dichiaratamente interpretative basta una dichiarazione a inizio sezione.

Se qualcosa non è stabilibile, viene scritto. Non aggirato con una formula vaga.

### Pipeline interna obbligatoria

Prima di formulare qualunque giudizio, la skill percorre internamente e in quest'ordine:

1. descrizione oggettiva di ciò che si vede, senza aggettivi valutativi;
2. mappatura dei pesi visivi e del percorso dell'occhio;
3. rilievo tecnico, osservato o stimato;
4. formulazione delle ipotesi di intenzione dell'autore.

Solo dopo questi quattro passaggi può valutare. Il verdetto sintetico può comunque comparire fin dalle prime righe della scheda: quello che non può accadere è che il giudizio preceda lo sguardo.

### Ancoraggio dei giudizi

- **Giudizi locali** (nitidezza, clipping, flare, elementi di disturbo, separazione figura e sfondo, intrusioni sui bordi): indicano sempre la zona dell'immagine che li giustifica. "In alto a sinistra", "sul bordo destro", "dietro la figura", "nel terzo inferiore".
- **Giudizi globali** (bilanciamento del bianco, contrasto complessivo, dominante cromatica): non hanno una zona, quindi devono dichiarare gli indizi visivi da cui sono ricavati. Non "il bianco è freddo", ma "i bianchi del muro virano al ciano mentre gli incarnati restano neutri, quindi la dominante è nelle alte luci e non globale".

### Vincolo anti normalizzazione

La skill non ottimizza automaticamente verso ordine, pulizia, nitidezza, simmetria o leggibilità. Il miglioramento proposto deve preservare o aumentare l'intenzione espressiva, anche quando questa dipende da caos, ambiguità, mosso, grana, disequilibrio o oscurità.

Un difetto tecnico che serve l'immagine non è un difetto: viene riconosciuto come scelta e valutato come tale. Vale in particolare per grana e sottoesposizione in chiave Moriyama, sfocatura in chiave Sieff, inclinazione volontaria, densità caotica in chiave Klein, tagli aggressivi. La domanda giusta non è "è pulito", ma "serve".

### Divieti anti invenzione

- mai inventare EXIF assenti;
- mai simulare istogrammi o misurazioni che i dati non consentono;
- mai dichiarare di riconoscere luoghi, persone o eventi senza certezza;
- mai attribuire citazioni ai fotografi senza certezza della fonte;
- mai dedurre la dimensione massima di stampa da un'anteprima;
- se il file è compresso o a bassa risoluzione, dichiararlo e limitare di conseguenza ogni giudizio su nitidezza, rumore e microdettaglio.

## La scheda completa: tredici sezioni

| # | Sezione | Cosa contiene |
|---|---|---|
| 1 | **Lettura a freddo** | cosa colpisce nei primi tre secondi, dove cade l'occhio, che percorso compie, cosa si perde per strada. Se l'immagine non regge, lo dice qui |
| 2 | **Ipotesi di intenzione** | da una a tre ipotesi su cosa cercava l'autore, con l'ipotesi più forte e gli indizi che la sostengono. Tutti i difetti rilevati dopo sono misurati contro questa ipotesi, non contro un canone implicito |
| 3 | **Scheda tecnica** | EXIF se presenti, tenuta delle alte luci, leggibilità delle ombre, piano focale, profondità di campo, nitidezza, microcontrasto, mosso, rumore, aberrazioni, diffrazione, bilanciamento del bianco, qualità e direzione della luce |
| 4 | **Geometria e composizione** | struttura portante, bilanciamento delle masse, spazio negativo, stratificazione, ritmo, simmetrie e rotture, gestione dei bordi, punto di vista, prospettiva, formato, direzione dello sguardo |
| 5 | **Soggetto, momento, espressione** | se era il soggetto giusto, se l'istante è quello di massima tensione, gesto, postura, relazione tra le figure. Con nota etica quando compaiono persone in condizione di fragilità o minori |
| 6 | **Lettura artistica e poetica** | dichiaratamente interpretativa. Cosa dice l'immagine oltre ciò che mostra. Chiude con un titolo proposto e un testo di massimo quattro righe, evocativo e non descrittivo |
| 7 | **Genealogia visiva** | da due a quattro fotografi del Novecento: quale problema visivo condividono con l'immagine, cosa l'immagine ha già, cosa le manca, come colmare la distanza |
| 8 | **Controanalisi** | tentativo esplicito di confutare la propria lettura, prima del verdetto |
| 9 | **Valutazione** | genere dichiarato, sette assi da 1 a 10, pesi per genere, calcolo mostrato, verdetto su cinque livelli |
| 10 | **Post produzione, piano operativo** | interventi in sequenza, ciascuno agganciato a un problema visivo. Ritagli alternativi con dichiarazione di cosa si perde. Parametri di output per web e stampa |
| 11 | **Pre scatto, la prossima volta** | istruzioni azionabili sul campo: posizione, distanza, focale, apertura, tempo, altezza della camera, attesa del momento |
| 12 | **La singola priorità** | una sola cosa, una sola frase. Nessun elenco, nessuna alternativa |
| 13 | **Esercizio** | un compito pratico e verificabile per la prossima uscita, eseguibile in una sola sessione |

### La controanalisi in dettaglio

È la sezione che distingue una critica da un'opinione. Prima del verdetto, la skill deve rispondere a cinque domande:

- ciò che sembra un errore compositivo potrebbe essere intenzionale?
- un elemento apparentemente inutile può avere funzione narrativa?
- il ritaglio che sto per proporre elimina informazione significativa?
- il riferimento storico è strutturale o solo somiglianza superficiale?
- la fotografia funziona forse proprio grazie a qualcosa che tecnicamente sarebbe considerato imperfetto?

L'esito è mostrato in massimo cinque righe. Deve essere visibile: se resta interno non è verificabile. Se smentisce la lettura iniziale, la lettura viene corretta, non difesa.

## Sistema di valutazione

Il genere viene dichiarato per primo, perché determina i pesi. Se il genere è ibrido, viene dichiarato quale set di pesi si applica e perché.

Sette assi, voto da 1 a 10 ciascuno: tecnica esecutiva, composizione e geometria, uso della luce, soggetto e momento, impatto emotivo, originalità, coerenza con un possibile corpus d'autore.

| Genere | Tec | Comp | Luce | Sogg | Emoz | Orig | Corpus |
|---|---|---|---|---|---|---|---|
| generico | 15 | 20 | 15 | 20 | 15 | 10 | 5 |
| street e reportage | 10 | 20 | 10 | 30 | 15 | 10 | 5 |
| ritratto | 15 | 15 | 20 | 25 | 15 | 5 | 5 |
| paesaggio e architettura | 20 | 25 | 25 | 10 | 10 | 5 | 5 |
| still life e studio | 25 | 25 | 25 | 10 | 5 | 5 | 5 |
| astratto e sperimentale | 5 | 20 | 15 | 10 | 20 | 25 | 5 |

I pesi non sono decorativi: nella street la tecnica pesa 10 e il soggetto 30, perché una foto di strada tecnicamente imperfetta ma sul momento giusto vale più di una impeccabile e vuota. Nello still life il rapporto si rovescia.

Il calcolo viene mostrato. Poi il verdetto, su cinque livelli:

**da scartare** · **da archivio** · **da portfolio** · **da stampa** · **da mostra**

Due righe di argomentazione, senza attenuazioni.

## I file di riferimento

I due file in [`references/`](critica-fotografica/references/) non vengono caricati insieme alla skill: vengono letti solo quando servono, per non occupare contesto inutilmente. È il meccanismo di progressive disclosure delle Agent Skill.

| File | Quando viene letto |
|---|---|
| [`canone.md`](critica-fotografica/references/canone.md) | prima di scrivere la sezione 7, per verificare pertinenza e condizioni di non applicabilità di ogni autore |
| [`postproduzione.md`](critica-fotografica/references/postproduzione.md) | prima di scrivere la sezione 10, per le strategie condizionali e i parametri di output |

### `canone.md` — il canone come problemi visivi

Non è un dizionario di associazioni. "Geometria uguale Cartier-Bresson, ombre uguale Fan Ho, colore uguale Leiter" è esattamente il modo in cui una critica diventa decorativa.

Ogni autore è codificato su cinque campi:

- **Problema**: il problema visivo che quell'autore ha affrontato;
- **Soluzione**: come lo ha risolto, in termini tecnici e operativi;
- **Pertinenza**: quando il riferimento regge;
- **Quando non citarlo**: il campo decisivo, letto sempre prima di inserire un nome nella scheda;
- **Errore dell'imitatore**: come si sbaglia tipicamente imitando quell'autore.

**Regola generale.** Un riferimento è legittimo solo se è possibile completare questa frase: *"il problema che questa immagine sta affrontando è lo stesso che [autore] affronta quando [situazione], e la differenza sta in [elemento verificabile]"*. Se la frase non si completa, si sta citando per prestigio, e un riferimento che non regge vale meno del silenzio.

Il canone è organizzato in dieci famiglie:

| # | Famiglia | Autori |
|---|---|---|
| 1 | Istante decisivo e geometria | Cartier-Bresson, Kertész, Erwitt, Doisneau e Ronis |
| 2 | Luce come struttura | Fan Ho, Brandt, Brassaï |
| 3 | Street densa e destabilizzata | Winogrand, Klein, Friedlander, Moriyama |
| 4 | Colore come soggetto | Leiter, Eggleston, Shore, Meyerowitz, Haas, Webb, Gruyaert, Fontana |
| 5 | Ritratto e presenza | Penn, Avedon, Arbus, Arnold |
| 6 | Reportage e coscienza sociale | Lange, W. Eugene Smith, Capa, Salgado, Koudelka, Larraín |
| 7 | Paesaggio e sistema zonale | Adams, Weston, Minor White, Strand |
| 8 | Sguardo italiano | Battaglia, Scianna, Berengo Gardin, Giacomelli, Ghirri, Jodice |
| 9 | Documento americano | Walker Evans, Robert Frank, Vivian Maier |
| 10 | Colore e narrazione internazionale | McCurry |

Alcuni campi *quando non citarlo* contengono giudizi netti e voluti. Su Arbus: non citarla per scatti rubati a persone in difficoltà, perché in quel caso il riferimento è un alibi, e va detto. Su Vivian Maier: la biografia non è un criterio critico, non citarla per il mito del ritrovamento. Su McCurry: va segnalato quando la costruzione rischia l'esotismo, perché è la critica più frequente rivolta a quel modello.

### `postproduzione.md` — strategie condizionali

Anche questo file non contiene ricette. "Texture +10, Chiarezza +15, Dehaze +5" è un look, non una correzione: applicato a tre fotografie diverse produce tre risultati sbagliati.

**Regola vincolante.** Prima di prescrivere un intervento va dichiarato quale problema visivo risolve. Se il problema non si identifica, l'intervento non si propone. Vale in particolare per chiarezza, texture, dehaze, dodge and burn e conversione in bianco e nero, che sono le cinque cose suggerite più spesso senza motivo.

Ogni voce ha lo stesso formato: **problema · obiettivo · strumento · intervallo di partenza · verifica**. I numeri sono punti di partenza da controllare a occhio, mai valori di ricetta.

L'ordine di intervento è fisso: correzioni globali, curve, maschere locali, dodge and burn, colore o conversione, grana, pulizia, ritaglio, output. Il ritaglio va deciso presto ma applicato tardi, perché cambiarlo dopo il lavoro locale costringe a rifare le maschere.

Le undici aree coperte:

1. esposizione e tono globale
2. alte luci e ombre
3. contrasto locale e volume
4. separazione tra figura e sfondo
5. colore
6. conversione in bianco e nero
7. nitidezza, rumore, grana
8. distrazioni e pulizia
9. geometria e ritaglio
10. output per web e per stampa
11. cosa non fare mai

Ogni intervento porta con sé il proprio criterio di verifica, che è la parte che manca quasi sempre nei tutorial. Sul dodge and burn: *"allontanati e guarda l'immagine ridotta al 25 per cento. Se vedi dove hai lavorato, hai lavorato troppo."* Sulla separazione figura e sfondo: *"la separazione buona non si vede."* Sulla coesione cromatica: *"chiudi gli occhi a metà. Se restano più di tre famiglie di colore riconoscibili, l'immagine è ancora dispersiva."*

Sulla dimensione di stampa vale la **regola dell'anteprima**: mai determinare la dimensione da un'immagine caricata in chat, che può essere una versione ridimensionata. Se le dimensioni pixel del file originale non sono note, la risposta è "non determinabile con affidabilità", seguita dai tre scenari a 300, 240 e 180 ppi.

La sezione 11, *cosa non fare mai*, è la contropartita di tutto il file:

- prescrivere un intervento senza aver nominato il problema che risolve;
- proporre un preset o un look al posto di una correzione;
- ottimizzare verso pulizia e ordine un'immagine la cui forza sta nel disordine, nel mosso, nella grana o nel buio;
- recuperare ombre e alte luci solo perché il cursore esiste;
- convertire in bianco e nero per salvare una fotografia debole;
- proporre valori come se fossero misurati.

## Modalità serie e portfolio

### Il format lock della modalità serie

La scheda a tredici sezioni **non** si applica a ogni immagine di una serie: su venti foto produrrebbe decine di migliaia di parole inutili. La struttura obbligatoria è un'altra:

1. scheda sintetica per ogni immagine, massimo 80 parole: cosa aggiunge alla serie, forza principale, limite principale, ruolo nella sequenza;
2. matrice comparativa in tabella: immagine, ruolo, registro tonale, densità visiva, forza da 1 a 10;
3. sequenza proposta, con motivazione dei passaggi e del ritmo;
4. eliminazioni, con motivo;
5. fotografie ponte e pause di respiro;
6. apertura e chiusura, argomentate;
7. ridondanze (immagini che dicono la stessa cosa) e lacune narrative;
8. scheda completa riservata a un numero di immagini chiave compreso tra 3 e 5.

### Portfolio non è serie

Sono criteri diversi, e la skill dichiara sempre quale sta applicando.

- **Portfolio**: ogni immagine è giudicata in autonomia. Regge da sola, senza didascalia e senza contesto? È rappresentativa dell'autore? Nessun credito per funzione di transizione.
- **Serie**: giudizio relazionale. Una fotografia debole in autonomia può essere necessaria come pausa, ponte, variazione di ritmo o abbassamento di tensione. In quel caso lo dice esplicitamente, invece di penalizzarla.

## Tono e stile

- registro informale, dà del tu;
- italiano, mai trattini lunghi: virgole, due punti o parentesi;
- vietati i complimenti generici: ogni lode indica l'elemento preciso che la giustifica;
- vietato il linguaggio da manuale: si parla di questa immagine, non della fotografia in generale;
- niente preamboli, niente riepiloghi finali del tipo "spero che questa analisi ti sia utile".

## Esempi di calibrazione

Sono nella skill come riferimento operativo, e chiariscono il livello richiesto meglio di qualunque descrizione.

> **Da evitare:** "Bella composizione, il soggetto è ben posizionato e la luce è gradevole."
>
> **Da produrre:** "La figura sta sul terzo destro ma il palo dietro la testa nasce esattamente dalla nuca: mezzo passo a sinistra lo avrebbe spostato nel vuoto della vetrina."

> **Da evitare:** "Ricorda Cartier-Bresson."
>
> **Da produrre:** "Il problema è lo stesso di Kertész a Meudon: due eventi su piani diversi che devono coincidere. Qui il secondo evento (l'uomo sullo sfondo) arriva mezzo secondo tardi e resta illeggibile."

## Esempi d’uso

Prompt pronti per ChatGPT, per critica completa, parere rapido, post-produzione, ritaglio, selezione di portfolio e stampa, sono disponibili in [examples/USAGE.md](examples/USAGE.md).

## Struttura del repository

```
.
├── README.md
├── LICENSE
└── critica-fotografica/
    ├── SKILL.md                      # istruzioni principali, sempre caricate
    └── references/
        ├── canone.md                 # 44 fotografi come problemi visivi risolti
        └── postproduzione.md         # strategie condizionali di post produzione
```

`SKILL.md` si apre con un frontmatter YAML che contiene `name` e `description`. La `description` è il meccanismo di attivazione: elenca esplicitamente i casi d'uso, incluse le richieste che non contengono la parola "critica", perché il modello decide di caricare la skill leggendo quel campo.

## Limiti noti

- **Nessuna misurazione reale.** Il modello vede un'immagine, non un file RAW. Istogrammi, valori di clipping e misure di nitidezza non sono calcolabili: la skill lo dichiara invece di simularli, ma resta un limite strutturale.
- **Compressione della chat.** Le immagini caricate in conversazione sono spesso ridimensionate e ricompresse. Ogni giudizio su microdettaglio, rumore e grana va letto in quella luce, e la skill lo segnala.
- **Il canone è parziale e situato.** 44 autori, con una sezione italiana ampia e una sottorappresentazione consapevole della fotografia contemporanea, di quella non occidentale e, in generale, delle autrici. È un canone di lavoro, non una storia della fotografia. Va esteso in base al proprio ambito.
- **La sezione 6 è interpretativa per costruzione.** Titolo e testo poetico non sono verificabili e non vanno letti come giudizio.
- **I voti sono uno strumento di confronto, non una misura.** Servono a ordinare le immagini di una stessa persona nel tempo, non a stabilire un valore assoluto.

## Personalizzare la skill

Tre punti di intervento naturali:

**Il canone.** Aggiungi autori in `references/canone.md` mantenendo i cinque campi, e soprattutto compilando *quando non citarlo* con la stessa durezza degli altri: è quel campo a impedire le citazioni decorative. Se lavori su un genere specifico (moda, sport, still life pubblicitario, fotografia scientifica), quel genere va aggiunto lì.

**I pesi di valutazione.** La tabella dei pesi in `SKILL.md` sezione 9 riflette una posizione critica precisa. Se non è la tua, cambiala: è una tabella, non un dogma. Puoi anche aggiungere righe per generi non previsti.

**Gli intervalli di post produzione.** I valori in `references/postproduzione.md` sono tarati su Lightroom e Capture One. Se lavori con altro software, adatta strumenti e intervalli mantenendo il formato problema, obiettivo, strumento, partenza, verifica.

## Criterio di successo

La scheda funziona se individua **almeno un elemento visivo non ovvio** che modifica o approfondisce la lettura dell'immagine, sia esso un limite, una forza o una tensione irrisolta.

Non serve trovare per forza un difetto: davanti a una fotografia eccellente, l'elemento non ovvio può essere la ragione per cui funziona.

## Licenza

[MIT](LICENSE).

I nomi dei fotografi citati in `references/canone.md` compaiono a fini di analisi critica e didattica. Nessuna opera è riprodotta in questo repository.


## Attribuzione

Skill ideata e attribuita esclusivamente a **Giuseppe Lupo**.
