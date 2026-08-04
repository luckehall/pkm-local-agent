# PKM Local Agent

Servizio locale per [PKM Cloud](https://pkm.iotzator.com) — estrae la traccia audio dai video
caricati in catalogazione e la trascrive con Whisper, entrambe le operazioni eseguite **sul tuo
PC**, mai sul server.

Questo repo esiste solo per ospitare l'eseguibile precompilato nelle
[Release](https://github.com/luckehall/pkm-local-agent/releases) — il codice sorgente vive nel
repo principale (privato) di PKM Cloud.

## Come funziona

1. Scarica l'eseguibile per il tuo sistema operativo dall'ultima release.
2. Avvialo (macOS/Linux: `chmod +x pkm-local-agent && ./pkm-local-agent`; Windows: doppio clic).
3. Lascialo in esecuzione — quando carichi un video su PKM Cloud, l'audio estratto e il testo
   trascritto vengono scritti automaticamente nel tuo vault Obsidian (cartella `_archive/`),
   tramite la Local REST API del plugin Obsidian (deve essere installato e attivo).

Nessuna configurazione richiesta: il servizio comunica solo con Obsidian in locale, non con
nessun server esterno.

## Piattaforme disponibili

- **macOS** (arm64) — disponibile
- Windows / Linux — non ancora pubblicati

## Requisiti

- [Obsidian](https://obsidian.md) con il plugin **Local REST API** installato e attivo
- Nessun altro prerequisito — ffmpeg e Whisper sono già inclusi nell'eseguibile
