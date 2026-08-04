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
2. Fatto — il servizio **parte da solo** subito dopo l'installazione e **ad ogni login del
   Mac** (nessun terminale da aprire, nessuna finestra visibile). Se vuoi verificare che sia
   attivo:
   ```bash
   curl http://127.0.0.1:27125/health
   ```
   I log si trovano in `~/Library/Logs/pkm-local-agent.log`.
3. Quando carichi un video su PKM Cloud, l'audio estratto e il testo trascritto vengono
   scritti automaticamente nel tuo vault Obsidian (cartella `_archive/`), tramite la Local
   REST API del plugin Obsidian (deve essere installato e attivo).

Nessuna configurazione richiesta: il servizio comunica solo con Obsidian in locale, non con
nessun server esterno.

### Fermare o disinstallare il servizio

```bash
launchctl bootout gui/$(id -u)/com.iotzator.pkm-local-agent   # ferma il servizio (finché non riavvii il Mac)
rm ~/Library/LaunchAgents/com.iotzator.pkm-local-agent.plist  # disabilita l'avvio automatico
sudo rm /usr/local/bin/pkm-local-agent                        # rimuove l'eseguibile
```

### Installazione manuale (avanzata, nessun avvio automatico)

Se preferisci non usare l'installer, puoi scaricare direttamente il binario
**`pkm-local-agent-macos-arm64`** dalla release:
```bash
chmod +x pkm-local-agent-macos-arm64
xattr -d com.apple.quarantine pkm-local-agent-macos-arm64   # sblocca Gatekeeper
./pkm-local-agent-macos-arm64
```
In questo caso il servizio va rilanciato a mano ad ogni sessione — nessun LaunchAgent viene
installato.

## Piattaforme disponibili

- **macOS** (arm64) — disponibile
- Windows / Linux — non ancora pubblicati

## Requisiti

- [Obsidian](https://obsidian.md) con il plugin **Local REST API** installato e attivo
- Nessun altro prerequisito — ffmpeg e Whisper sono già inclusi nell'eseguibile
