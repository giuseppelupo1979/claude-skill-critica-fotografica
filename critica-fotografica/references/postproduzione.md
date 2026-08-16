# Post produzione: strategie condizionali

Questo file non contiene ricette. "Texture +10, Chiarezza +15, Dehaze +5" è un
look, non una correzione: applicato a tre fotografie diverse produce tre risultati
sbagliati.

**Regola vincolante.** Prima di prescrivere un intervento, dichiara quale problema
visivo risolve. Se non riesci a identificare il problema, l'intervento non si
propone. Questo vale in particolare per chiarezza, texture, dehaze, dodge and
burn e conversione in bianco e nero, che sono le cinque cose che vengono
suggerite più spesso senza motivo.

**Formato di ogni voce.** Problema, obiettivo, strumento, intervallo di partenza,
verifica. I numeri sono punti di partenza da controllare a occhio, mai valori da
applicare.

**Ordine di intervento.** Correzioni globali, curve, maschere locali, dodge and
burn, colore o conversione, grana, pulizia, ritaglio, output. Il ritaglio va
deciso presto ma applicato tardi: cambiarlo dopo il lavoro locale costringe a
rifare le maschere.

## Indice

1. Esposizione e tono globale
2. Alte luci e ombre
3. Contrasto locale e volume
4. Separazione tra figura e sfondo
5. Colore
6. Conversione in bianco e nero
7. Nitidezza, rumore, grana
8. Distrazioni e pulizia
9. Geometria e ritaglio
10. Output per web e per stampa
11. Cosa non fare mai

---

## 1. Esposizione e tono globale

**Immagine complessivamente chiusa, i mezzitoni cadono troppo in basso e il
soggetto non emerge**
- Obiettivo: riportare il punto medio dove serve, senza schiarire i neri.
- Strumento: Esposizione in Lightroom o Capture One, poi curva a S leggera con il
  punto nero ancorato.
- Partenza: da +0,20 a +0,60 EV, poi si valuta.
- Verifica: i neri più profondi devono restare dove erano. Se si sono alzati,
  riabbassa il punto nero della curva invece di ridurre l'esposizione.

**Immagine piatta, nessun bianco e nessun nero reale**
- Obiettivo: ristabilire i due estremi, non aggiungere contrasto ovunque.
- Strumento: cursori Bianchi e Neri (Lightroom), o punti estremi dei Livelli
  (Capture One).
- Partenza: porta i Bianchi fin quasi al clipping e riportali indietro di due o
  tre punti; stessa cosa sui Neri.
- Verifica: guarda l'immagine, non l'istogramma. Una fotografia in nebbia deve
  restare in nebbia: il contrasto pieno non è sempre l'obiettivo.

**Immagine chiaramente sovraesposta in ripresa**
- Se le alte luci sono clippate su tutti e tre i canali, l'informazione non c'è.
  Non fingere di recuperarla: dichiaralo come limite e valuta se la zona bruciata
  disturba o se può diventare bianco puro accettabile.

## 2. Alte luci e ombre

**Alte luci prossime alla saturazione in una zona circoscritta**
- Obiettivo: recuperare struttura solo lì, senza appiattire tutto.
- Strumento: maschera lineare o radiale sulla zona, poi Luci in negativo dentro la
  maschera. Non il cursore Luci globale.
- Partenza: da -20 a -45 dentro la maschera.
- Verifica: al 100 per cento, controlla che non compaia un alone sul bordo della
  maschera. Se compare, aumenta la sfumatura.

**Ombre chiuse in cui serve leggibilità**
- Obiettivo: aprire quel tanto che basta a far leggere la forma, non a mostrare
  tutto.
- Strumento: Ombre, o meglio una maschera di luminosità sulle zone scure.
- Partenza: da +15 a +35.
- Verifica: oltre una certa soglia le ombre diventano grigie e l'immagine perde
  peso. Confronta con la versione precedente ogni dieci punti. Nei notturni e nei
  bianco e nero contrastati la risposta corretta è spesso zero.

## 3. Contrasto locale e volume

**Il soggetto è correttamente esposto ma sembra piatto, senza volume**
- Obiettivo: ricostruire il modellato con la luce, non con la chiarezza.
- Strumento: dodge and burn. In Photoshop: livello nuovo riempito di grigio 50 per
  cento in modalità Sovrapponi, pennello morbido con flusso basso. In Lightroom:
  maschere a pennello con esposizione minima.
- Partenza: flusso dal 2 al 5 per cento, molte passate leggere; in Lightroom da
  +0,10 a +0,25 EV per zona.
- Verifica: allontanati e guarda l'immagine ridotta al 25 per cento. Se vedi dove
  hai lavorato, hai lavorato troppo.

**Superficie senza texture (roccia, corteccia, muro) che dovrebbe averla**
- Strumento: Texture (Lightroom) o Struttura (Capture One), applicato in maschera
  sulla superficie, mai globale se ci sono volti nell'inquadratura.
- Partenza: da +10 a +25 nella maschera.
- Verifica: controlla i volti e il cielo. Se hai applicato globalmente, la pelle
  si indurisce e il cielo si sporca.

## 4. Separazione tra figura e sfondo

**Il soggetto deve emergere senza sembrare localmente schiarito**
- Obiettivo: aumentare la separazione tonale, non l'esposizione.
- Strumento: maschera soggetto, poi due interventi complementari: leggero aumento
  di esposizione sul soggetto e leggera riduzione sullo sfondo. Sfumatura alta.
- Partenza: da +0,15 a +0,35 EV sul soggetto, da -0,10 a -0,25 EV sullo sfondo,
  con eventuale compensazione delle alte luci.
- Verifica: al 100 per cento sul contorno. Se compare un bordo chiaro attorno alla
  figura, riduci l'intensità e aumenta la sfumatura. La separazione buona non si
  vede.

**Lo sfondo è cromaticamente troppo vicino al soggetto**
- Strumento: desaturazione selettiva sullo sfondo, o spostamento di tinta di pochi
  gradi via HSL o editor colore avanzato.
- Partenza: da -10 a -25 di saturazione sulla gamma dominante dello sfondo.
- Verifica: controlla che gli incarnati non siano toccati dalla stessa gamma.

## 5. Colore

**Dominante nelle alte luci con incarnati corretti**
- Non correggere con il bilanciamento del bianco globale: sposteresti anche ciò
  che è giusto.
- Strumento: curva di viraggio sulle alte luci, o Editor colore avanzato con
  selezione stretta.
- Partenza: correzione di pochi punti, verificando su un grigio noto nella scena.

**Colore corretto ma senza coesione**
- Obiettivo: ridurre il numero di famiglie cromatiche presenti.
- Strumento: HSL o editor colore, riducendo saturazione e avvicinando le tinte
  secondarie a quella dominante.
- Verifica: chiudi gli occhi a metà. Se restano più di tre famiglie di colore
  riconoscibili, l'immagine è ancora dispersiva.

## 6. Conversione in bianco e nero

**Prima domanda, sempre: perché.** La conversione è legittima se il colore
disturba la lettura della forma, se le famiglie cromatiche sono troppe e
incoerenti, o se il soggetto è materia e struttura. Non è legittima come salvataggio
di una immagine debole: il bianco e nero non aggiunge senso, lo cambia. Se il
colore è portante (Leiter, Ghirri, Gruyaert), la conversione distrugge l'immagine
e va sconsigliata esplicitamente.

**Conversione con controllo sulle famiglie tonali**
- Strumento: mixer bianco e nero (Lightroom) o Silver Efex con control points.
- Partenza: parti dal canale della tinta dominante. Cieli: da -15 a -35 sul blu.
  Incarnati: interventi minimi su arancio e rosso, la pelle si degrada in fretta.
- Verifica: cerca zone che collassano nello stesso grigio. Se due elementi
  adiacenti diventano indistinguibili, hai perso separazione: recuperala con il
  mixer, non con il contrasto globale.

**Grana**
- Aggiungila solo se serve a unificare una immagine già rumorosa o a coerenza con
  un corpus dichiarato. Mai come segnale di autenticità.
- Partenza: quantità da 10 a 25, dimensione bassa per stampe piccole, media per
  stampe grandi.

## 7. Nitidezza, rumore, grana

**Rumore cromatico e di luminanza su file ad alti ISO**
- Strumento: DxO PureRAW o denoise AI prima di qualunque altro intervento, perché
  agisce sul demosaicizzato.
- Verifica: controlla le zone di transizione e i capelli. La riduzione eccessiva
  produce superfici di cera. Preferisci un residuo di rumore a una pelle plastica.

**Nitidezza**
- Distingui sempre: nitidezza di cattura (correzione dell'ottica), nitidezza
  creativa (locale, sul soggetto), nitidezza di output (dipende dal supporto).
  Sono tre passaggi diversi e non si sostituiscono.
- La nitidezza di output si applica alla fine, sul file già ridimensionato.

## 8. Distrazioni e pulizia

**Elemento di disturbo sul bordo**
- Prima di rimuoverlo, passa dalla controanalisi: ha funzione? In Friedlander
  l'intrusione è il soggetto.
- Se non ha funzione: prima prova a ritagliarlo fuori, poi a scurirlo, e solo come
  ultima scelta a clonarlo. Il ritaglio è più onesto e non lascia tracce.

**Rimozione di elementi interni alla scena**
- Sconsigliata nella fotografia documentaria e di strada: cambia il documento. Se
  la fotografia appartiene a un progetto documentario, dillo e non proporla.

## 9. Geometria e ritaglio

**Orizzonte inclinato**
- Prima stabilisci se l'inclinazione è voluta. In Winogrand o Larraín raddrizzare
  è un errore critico, non una correzione.
- Se non è voluta: raddrizza e verifica cosa perdi ai bordi. Se perdi un elemento
  strutturale, il ritaglio non conviene.

**Verticali cadenti in architettura**
- Correzione prospettica parziale, non totale: la correzione al 100 per cento
  spesso produce un effetto innaturale e allarga la base dell'edificio.
- Partenza: correggi tra il 60 e l'80 per cento della deviazione.

**Proposta di ritagli alternativi**
- Per ogni ritaglio proposto dichiara: rapporto d'aspetto, cosa guadagna, cosa
  perde. Un ritaglio che non perde nulla di solito non serviva.
- Rapporti utili da considerare: 3:2 nativo, 4:5 per la figura verticale, 1:1 per
  la struttura centrale, 16:9 per la stratificazione orizzontale.

## 10. Output per web e per stampa

**Web**
- sRGB, 8 bit, lato lungo da 1600 a 2400 pixel, nitidezza di output per schermo
  moderata. Verifica il risultato al 100 per cento e alla dimensione reale di
  visualizzazione.

**Stampa fine art**
- File a 16 bit, spazio ampio (Adobe RGB o ProPhoto) fino all'export finale.
- Soft proofing con il profilo della carta prima di decidere qualunque cosa sulle
  ombre.
- Su carta opaca il nero massimo è più chiaro che su baritata lucida: le ombre
  vanno alzate rispetto alla versione da schermo, tipicamente di poco, e il
  contrasto locale nelle zone scure va rinforzato.
- Nitidezza di output specifica per supporto, applicata dopo il ridimensionamento.
- Compensazione del punto di nero attiva, intento di rendering percettivo per
  immagini con colori fuori gamut, relativo colorimetrico per il resto.

**Dimensione massima di stampa**
- Regola dell'anteprima: non determinare mai la dimensione di stampa da una
  immagine caricata in chat, che può essere una versione ridimensionata.
- Se le dimensioni pixel del file originale non sono note, scrivi "non
  determinabile con affidabilità" e fornisci i tre scenari:
  - 300 ppi: qualità di riferimento per osservazione ravvicinata.
  - 240 ppi: standard robusto per stampe fine art di medio formato.
  - 180 ppi: accettabile per stampe grandi osservate a distanza.
- Presenta il calcolo come lato lungo in pixel diviso ppi, in centimetri.

## 11. Cosa non fare mai

- Prescrivere un intervento senza aver nominato il problema che risolve.
- Proporre un preset o un "look" al posto di una correzione.
- Ottimizzare verso pulizia, nitidezza e ordine una immagine la cui forza sta nel
  disordine, nel mosso, nella grana o nel buio.
- Recuperare ombre e alte luci solo perché il cursore esiste.
- Convertire in bianco e nero per salvare una fotografia debole.
- Proporre valori come se fossero misurati: sono sempre punti di partenza.
