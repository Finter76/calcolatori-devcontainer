# DevContainer per Calcolatori Elettronici

Questo è un ambiente di sviluppo containerizzato per il corso di [Calcolatori Elettronici](https://calcolatori.iet.unipi.it/) della Scuola di Ingegneria dell'Università di Pisa.

## Caratteristiche

Il DevContainer include tutti gli strumenti necessari per completare le esercitazioni e la prova pratica del corso, tra cui:

- **libce**: Libreria di supporto per gli esempi I/O e il nucleo
- **QEMU modificato**: Versione patchata di QEMU per il corso
- **Toolchain completa**: Include compilatori e strumenti necessari (gcc, g++, etc.)
- **Tool per scaricare esami**: Utility per scaricare automaticamente le prove d'esame passate

## Utilizzo dello script `scarica-esame`

Il container include uno script `scarica-esame` per gestire il download degli esami passati:

```bash
# Visualizzare tutte le date disponibili
scarica-esame list

# Scaricare l'esame di una data specifica
scarica-esame yyyy-mm-dd
```

## Ambiente preconfigurato

Questo DevContainer include:

- **Build tools**: gcc/g++ con supporto multilib per compilazione a 32/64 bit
- **Debugger**: GDB per il debug dei programmi
- **Librerie**: Tutte le dipendenze necessarie per compilare ed eseguire il nucleo e gli esempi
- **Percorsi**: PATH già configurato per utilizzare gli strumenti del corso

## Come iniziare

1. Assicurati di avere Docker e VS Code con l'estensione Dev Containers installati
2. Clona questo repository e aprilo in VS Code
  - Attenzione, per chi ha MACOS, per clonare usare `git clone --branch macos <linkHTTP>`, altrimenti clonate la repo main
3. Quando richiesto, seleziona "Reopen in Container"
4. Usa lo script `scarica-esame` per scaricare gli esami di tuo interesse
5. Inizia a lavorare sugli esercizi!

## Fix Visualizzazione
**Interfaccia Grafica Integrata:** È stata integrata la feature `desktop-lite`, che fornisce un ambiente desktop virtuale accessibile comodamente dal browser per visualizzare l'output grafico di QEMU.
In caso non si voglia visualizzare esternamente QEMU, ma ci si accontenta del terminale in VSCode, lanciare lo script `boot -c`; l'output sarà **esclusivamente in modalità testo**.

### Come visualizzare lo schermo di QEMU su Browser
Una volta che il container è completamente avviato e si lancia lo script di `boot`, la finestra di QEMU verrà renderizzata nel desktop virtuale del container. 
Per interagire con la macchina virtuale:
1. Apri il tuo browser web preferito.
2. Vai all'indirizzo: [http://localhost:6080](http://localhost:6080) (la porta viene inoltrata automaticamente da VS Code).

### Troubleshooting: Errore Certificati / SSL in fase di build
Se durante la prima creazione del container (nello specifico durante il download della feature `desktop-lite`) il processo fallisce con un errore simile a **`unable to get issuer certificate`**, significa che la rete a cui sei connesso o il sistema macOS sta intercettando e bloccando il download sicuro di Node.js.

Per risolvere, si può applicare **una** di queste due soluzioni:
1. Apri le Impostazioni di VS Code, cerca **System Certificates** e disabilita/togli la spunta all'opzione `Http: System Certificates`. Riavvia VS Code chiudendolo completamente e lancia di nuovo il Rebuild. Dopo il Rebuild, **Riabilita l'opzione**.
2. Commenta nel file `devcontainer.json` la riga contenente `"ghcr.io/mcr.microsoft/devcontainers/features/desktop-lite:1": {}` (ciò renderà inutilizzabile il collegamento con la finestra di QEMU virtuale)

## Licenza e contributi

Questo progetto è rilasciato sotto licenza [GPLv3](https://www.gnu.org/licenses/gpl-3.0.txt).

Pull Request da parte degli studenti sono benvenute!
In caso di problemi o suggerimenti, sentiti libero di aprire una Issue sul repository.
I contributi degli studenti sono particolarmente apprezzati per migliorare questo ambiente e renderlo più utile per i futuri studenti del corso.
