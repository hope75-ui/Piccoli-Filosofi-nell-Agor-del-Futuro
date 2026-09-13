# ⚠️ Nota per chi modifica le immagini del repository

`index.html` carica tutte le illustrazioni da `images/`, organizzata in **tre
sottocartelle**, una per ogni storia, nominate con il titolo della storia stessa.
I percorsi sono scritti "a mano" dentro lo script (variabile `storiesData`, in
fondo a `index.html`) e nelle tabelle del `README.md`.

**Se rinomini una cartella o un file in `images/` senza aggiornare questi
riferimenti, quell'illustrazione smette di comparire online** — il sito resta
comunque funzionante (nessun errore visibile), ma il riquadro dell'immagine
resterà vuoto o mostrerà l'icona di rottura del browser.

## Struttura e file attesi (32 immagini in 3 cartelle)

| Cartella | Storia | Copertina | Pagine |
|---|---|---|---|
| `images/1-la-montagna-doro/` | 1 — Il Segreto della Montagna d'Oro | `cover.jpg` | `scene-01.jpg` … `scene-09.jpg` (9 pagine) |
| `images/2-la-bilancia-magica/` | 2 — La Bilancia di Mezzonia e il Drago Pesante | `cover.jpg` | `scene-01.jpg` … `scene-10.jpg` (10 pagine) |
| `images/3-il-fiore-dei-tre-amici/` | 3 — Il Segreto del Fiore dell'Amicizia | `cover.jpg` | `scene-01.jpg` … `scene-10.jpg` (10 pagine) |

Ogni percorso è usato in **due punti diversi** del progetto — se lo cambi, aggiornali entrambi:

1. **`index.html`** → nella variabile `storiesData` (campo `img:` di ogni pagina, e i tre `<img src="...">` nei pulsanti di selezione storia).
2. **`README.md`** → nelle tabelle delle sezioni 9, 9bis, 9ter (i racconti integrali).

## Come rinominare in sicurezza

Non modificare i percorsi a mano uno per uno: usa "trova e sostituisci" su
**entrambi** i file (`index.html` e `README.md`) con lo stesso vecchio percorso
e il nuovo, così i due punti restano sincronizzati. Ad esempio, per rinominare
la cartella della Storia 2:

- cerca `images/2-la-bilancia-magica/`
- sostituisci con il nuovo nome cartella scelto
- ripeti l'operazione sia in `index.html` sia in `README.md`
- rinomina fisicamente anche la cartella dentro `images/`

## Come verificare che non manchi nulla

Dopo qualsiasi modifica, apri il mockup in un browser e controlla visivamente le
tre storie nella sezione **Storybook** (copertina + tutte le pagine). Per un
controllo da riga di comando (utile prima di un commit), da dentro la cartella
del repository:

```bash
# Elenca i percorsi immagine citati in index.html ma assenti su disco
grep -oE 'images/[A-Za-z0-9_/-]+\.jpg' index.html | sort -u | \
  while read f; do [ -f "$f" ] || echo "MANCANTE: $f"; done
```

Se il comando non stampa nulla, tutti i riferimenti sono validi.
