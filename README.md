# PKM Local Agent

Servizio locale per [PKM Cloud](https://pkm.iotzator.com) — estrae la traccia audio dai video
caricati in catalogazione e la trascrive con Whisper, entrambe le operazioni eseguite **sul tuo
PC**, mai sul server.

Questo repo esiste solo per ospitare l'eseguibile precompilato nelle
[Release](https://github.com/luckehall/pkm-local-agent/releases) — il codice sorgente vive nel
repo principale (privato) di PKM Cloud.

## Come funziona

1. Scarica **`pkm-local-agent-installer.pkg`** dall'ultima release e aprilo.
   macOS bloccherà l'apertura la prima volta ("impossibile verificare lo sviluppatore") — è
   normale, l'eseguibile non è firmato con un certificato Apple a pagamento. Sblocca con
   **tasto destro sul file → Apri → Apri** (una volta sola), poi segui il wizard
   "Continua → Installa" (richiede la password del tuo Mac).
2. Apri un **Terminale** e lancia:
   ```bash
   pkm-local-agent
   ```
3. Lascia la finestra aperta — quando carichi un video su PKM Cloud, l'audio estratto e il
   testo trascritto vengono scritti automaticamente nel tuo vault Obsidian (cartella
   `_archive/`), tramite la Local REST API del plugin Obsidian (deve essere installato e
   attivo).

Nessuna configurazione richiesta: il servizio comunica solo con Obsidian in locale, non con
nessun server esterno.

### Installazione manuale (avanzata)

Se preferisci non usare l'installer, puoi scaricare direttamente il binario
**`pkm-local-agent-macos-arm64`** dalla release:
```bash
chmod +x pkm-local-agent-macos-arm64
xattr -d com.apple.quarantine pkm-local-agent-macos-arm64   # sblocca Gatekeeper
./pkm-local-agent-macos-arm64
```

## Piattaforme disponibili

- **macOS** (arm64) — disponibile
- Windows / Linux — non ancora pubblicati

## Requisiti

- [Obsidian](https://obsidian.md) con il plugin **Local REST API** installato e attivo
- Nessun altro prerequisito — ffmpeg e Whisper sono già inclusi nell'eseguibile
