# Analisi degli infortuni sul lavoro in Italia

Analisi **end-to-end** degli infortuni sul lavoro in Italia per **settore, regione e anno**, con stima dei **costi**, a supporto di una decisione di investimento in prevenzione. Il progetto copre l'intera filiera: dall'acquisizione e analisi dei dati con **Python** alla presentazione degli insight con una dashboard interattiva in **Power BI**.

---

## Contesto

Il progetto nasce da una richiesta reale: una startup del settore **sicurezza sul lavoro**, che sviluppa un dispositivo di protezione individuale (DPI), aveva bisogno di capire **su quali settori e regioni** concentrare il proprio investimento.

L'analisi in questo repository risponde a quella domanda dal lato dei **dati**: individua dove si concentrano gli infortuni, in quali comparti, e quanto costano. Le informazioni riservate del cliente e del prodotto non sono incluse: qui è documentata solo l'analisi dei dati pubblici e la relativa dashboard di insight.

## Domande di analisi

1. Quanti infortuni si registrano per settore, regione e anno?
2. Come si distribuisce il rischio una volta rapportato al numero di imprese/addetti?
3. Quali comparti combinano alta frequenza di infortuni e alti costi?
4. Su quali settori/regioni conviene indirizzare gli investimenti in prevenzione?

## Fonti dati

L'analisi combina tre fonti pubbliche:

| Fonte | Cosa fornisce | Formato | Aggiornamento |
|-------|---------------|---------|---------------|
| **INAIL** | Infortuni sul lavoro (per regione, settore, anno) | CSV (zip) | Semestrale (luglio / dicembre) |
| **ISTAT ASIA** | Imprese e addetti per settore | *(in lavorazione)* | *(in lavorazione)* |
| **INPS** | Retribuzioni / costo del lavoro per settore | *(in lavorazione)* | *(in lavorazione)* |

## Metodologia

L'approccio privilegia la **verifica empirica** delle fonti prima di costruire il dataset finale:

- **Scelta della fonte INAIL:** confronto tra API JSON e file CSV scaricabili. L'API è stata testata su tutte le combinazioni anno/mese (2001–2025) e scartata perché copre solo una finestra parziale e recente; si è optato per i file CSV, più completi.
- **Analisi della struttura dei file:** verifica su file campione di duplicati interni, periodo di accadimento coperto e sovrapposizione tra le versioni semestrali dello stesso anno.
- **Regola della finestra mobile:** confermato empiricamente che ogni file copre 5 anni di accadimento; su questa base sono stati scelti i file minimi necessari a coprire l'intero storico senza sovrapposizioni né buchi.
- **Perimetro finale INAIL:** accadimento **2014–2024** (11 anni), **~6,9 milioni di righe**, nessuna sovrapposizione, nessun buco.

## Dalla dati alla decisione: la dashboard Power BI

La fase finale del progetto traduce l'analisi in una **dashboard interattiva in Power BI**, pensata per chi deve prendere le decisioni di investimento. La dashboard incrocia le tre fonti per evidenziare:
- i settori e le regioni a maggiore **frequenza** di infortuni;
- il **rischio relativo** (infortuni rapportati a imprese/addetti);
- la **stima dei costi** associati, per individuare dove la prevenzione ha maggiore impatto.

> Nel repository sono inclusi solo gli elementi relativi all'analisi dei dati (infortuni per settore, regione e costi). Il materiale riservato del cliente e la scheda prodotto non sono pubblicati.

## Struttura del progetto

```
Infortuni_per_settore_ITA/
├── Analisi_infortuni_sul_lavoro_ITA.ipynb   # notebook principale (acquisizione + analisi)
├── README.md                                # questo file
├── requirements.txt                         # librerie necessarie
├── dashboard/                                # dashboard Power BI (.pbix) — da aggiungere
└── dati_grezzi_inail/                        # dati scaricati (NON versionati)
```

> **Nota:** i dati grezzi (file `.zip` e CSV consolidato) non sono inclusi nel repository perché pesanti e riscaricabili tramite il notebook. Il notebook li scarica e li ricostruisce in autonomia.

## Come eseguire il progetto

1. Creare e attivare un ambiente virtuale Python.
2. Installare le librerie:
   ```
   pip install -r requirements.txt
   ```
3. Aprire `Analisi_infortuni_sul_lavoro_ITA.ipynb` in VS Code (o Jupyter) e selezionare l'ambiente come kernel.
4. Eseguire le celle in ordine: il notebook scarica i dati e costruisce il dataset finale.
5. La dashboard Power BI (`.pbix`) si apre con **Power BI Desktop** e utilizza il dataset prodotto dal notebook.

**Tecnologie:** Python (pandas, numpy, matplotlib, seaborn, requests), Jupyter Notebook, Power BI (DAX, Power Query).

## Stato del progetto

🚧 **Work in progress.**

- [x] Acquisizione e consolidamento dati INAIL (infortuni, 2014–2024)
- [ ] Acquisizione dati ISTAT ASIA (imprese e addetti)
- [ ] Acquisizione dati INPS (retribuzioni)
- [ ] Pulizia e decodifica (tipologiche INAIL: ATECO, province, esito)
- [ ] Analisi incrociata e calcolo indicatori di rischio/costo
- [ ] Visualizzazioni e sintesi degli insight
- [ ] Dashboard interattiva in Power BI

## Autore

**Geson Bani** — progetto sviluppato nell'ambito del percorso di formazione in data analysis.