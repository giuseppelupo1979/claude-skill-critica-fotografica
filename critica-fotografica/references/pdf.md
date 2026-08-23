# Esportazione della scheda in PDF

Ricetta operativa per trasformare una scheda già scritta in un PDF impaginato.
Non è un passaggio automatico: si esegue solo dopo che l'utente ha risposto di sì
alla domanda finale prevista dalla sezione "Consegna e proposta di PDF" della
SKILL.

## Regola di destinazione

Il PDF va salvato **nella stessa posizione del file originale analizzato**.

1. Ricava la cartella del file sorgente dal percorso che hai ricevuto.
2. Se il file è su una cartella collegata del computer dell'utente, costruisci il
   PDF nello spazio di lavoro, poi consegnalo con `SendUserFile` e scrivilo in
   quella cartella con `device_commit_files`, allo stesso livello dell'immagine.
3. Se il file è stato caricato in conversazione, scrivi il PDF nella stessa
   cartella dell'immagine caricata e consegnalo con `SendUserFile`.
4. Nome del file: stesso nome dell'immagine con suffisso `_critica.pdf`. Se
   l'immagine ha un nome generato dal sistema e privo di senso, usa il titolo
   proposto nella sezione 6, ripulito, più `_critica.pdf`.
5. Non sovrascrivere mai un PDF esistente con lo stesso nome: aggiungi `_v2`,
   `_v3` e così via.

## Costruzione

Percorso consigliato: Markdown della scheda, conversione in HTML con pandoc,
impaginazione con un foglio di stile per la stampa, rendering in PDF con
Chromium headless.

```bash
pandoc scheda.md -f markdown -t html5 -o body.html
# poi inserisci body.html nel template qui sotto e rendi
chromium --headless --disable-gpu --no-sandbox --no-pdf-header-footer \
  --print-to-pdf=uscita.pdf file:///percorso/assoluto/scheda.html
```

Se Chromium non è disponibile, ripiega su `wkhtmltopdf`, e solo come ultima
scelta su reportlab (che però non gestisce bene questo tipo di impaginazione).

Incorpora tutte le immagini come data URI in base64, così il file HTML resta
autonomo e il rendering non dipende dai percorsi.

## Contenuto obbligatorio del PDF

- **Copertina**: la fotografia analizzata a piena pagina o quasi, il titolo
  proposto nella sezione 6, la riga dei dati di ripresa reali (solo quelli letti
  dagli EXIF, mai inventati), genere, voto e verdetto.
- **Tutte le sezioni della scheda**, nell'ordine in cui sono state scritte.
- **Da una a tre figure di supporto**, ritagliate dal file originale, ciascuna con
  didascalia che dichiara cosa dimostra. Le più utili: il dettaglio che prova
  dove è caduto il fuoco, la zona che giustifica il rilievo principale, la
  simulazione del ritaglio preferito.
- La tabella della valutazione con il calcolo visibile.

Nessuna sezione va abbreviata per far stare il PDF in meno pagine.

## Template di stile

Formato A4, margini 20/18/18/18 mm, serif per il testo (Charter, in ripiego
DejaVu Serif), corpo fra 10 e 10,5 punti, interlinea 1,5, testo giustificato.
Titoli di sezione con filetto sottile sotto, titoli di terzo livello in maiuscoletto
spaziato. Copertina su fondo scuro. Tabelle con righe sottili e totale in grassetto.
Didascalie a 8 punti in grigio.

```css
@page { size: A4; margin: 20mm 18mm 18mm 18mm; }
@page :first { margin: 0; }
body { font-family: "Bitstream Charter","Charter","DejaVu Serif",serif;
       font-size: 10.4pt; line-height: 1.52; color: #17181a; margin: 0; }
.cover { page-break-after: always; height: 297mm; background: #0e0f11; color: #f2efe9; position: relative; }
.cover img { width: 100%; height: 197mm; object-fit: cover; object-position: 50% 22%; display: block; }
.cover .kicker { font-size: 8.4pt; letter-spacing: .22em; text-transform: uppercase; color: #a9a196; }
.cover h1 { font-size: 27pt; line-height: 1.12; font-weight: 600; }
h2 { font-size: 12.4pt; margin: 9mm 0 2.6mm 0; padding-bottom: 1.6mm;
     border-bottom: .6pt solid #c9c2b6; font-weight: 600; page-break-after: avoid; }
h3 { font-size: 10.3pt; margin: 5.5mm 0 1.6mm 0; font-weight: 600; color: #4a453d;
     text-transform: uppercase; letter-spacing: .08em; page-break-after: avoid; }
p { margin: 0 0 2.7mm 0; text-align: justify; hyphens: auto; }
blockquote { margin: 4mm 0 4mm 6mm; padding-left: 5mm; border-left: 1.6pt solid #b8a98c;
             font-style: italic; }
table { width: 100%; border-collapse: collapse; font-size: 9.4pt; page-break-inside: avoid; }
th { text-align: left; border-bottom: .8pt solid #17181a; padding: 1.4mm 2mm;
     font-size: 8.4pt; text-transform: uppercase; letter-spacing: .06em; }
td { border-bottom: .3pt solid #d8d3ca; padding: 1.4mm 2mm; }
tr:last-child td { border-bottom: .8pt solid #17181a; font-weight: 600; }
figure { margin: 5mm 0 6mm 0; page-break-inside: avoid; }
figure.duo { display: flex; gap: 4mm; }
figure.duo div { flex: 1 1 0; min-width: 0; }
figure img { width: 100%; display: block; }
figure.single { text-align: center; }
figure.single img { max-height: 92mm; width: auto; margin: 0 auto; }
figcaption { font-size: 8.2pt; line-height: 1.42; color: #6a645b; margin-top: 2mm; text-align: left; }
```

## Trappola da evitare, verificata sul campo

Se la copertina è un contenitore con testo chiaro su fondo scuro, **il contenitore
va chiuso prima del corpo della scheda**, e il corpo va avvolto in un elemento
proprio (per esempio `<main>`) con il colore del testo dichiarato esplicitamente.
Se il div della copertina resta aperto, tutto il documento eredita il colore
chiaro: la prima pagina sembra corretta e dalla seconda in poi il testo è quasi
bianco su bianco, cioè illeggibile, e il PDF sembra fatto di pagine vuote.

Non montare mai l'HTML finale ritagliando stringhe di un template con indici di
`index()` o simili: genera esattamente questo errore. Costruisci copertina, stile
e corpo come pezzi separati e concatenali.

## Verifica prima di consegnare il PDF

- Apri il PDF e controlla almeno la copertina, una pagina di testo e la pagina
  della tabella, rendendole in immagine.
- Nessuna pagina quasi vuota causata da una figura che non entra: se capita,
  riduci l'altezza massima della figura o spostala.
- **Controllo obbligatorio di leggibilità**: rendi in immagine almeno la pagina 2
  e una pagina centrale e misura i pixel scuri. Una pagina di testo normale ha fra
  il 3 e il 13 per cento di pixel sotto 120 di luminanza. Se il valore è vicino a
  zero, il testo è chiaro su bianco e il PDF non va consegnato.
- Nessuna pagina bianca non voluta.
- Nessun trattino lungo nel testo.
- Il numero di pagine e il percorso di salvataggio vanno dichiarati all'utente in
  una riga sola.
