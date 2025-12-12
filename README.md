# Analisi dei Ritardi dei Voli – Esercizio Finale

Questo progetto analizza i ritardi dei voli negli Stati Uniti, esplorando la distribuzione dei ritardi e i principali fattori che li influenzano. Vengono utilizzati grafici statistici e tecniche di visualizzazione per comprendere pattern stagionali, confrontare compagnie aeree e analizzare l’impatto del traffico aereo sui ritardi.

## Dataset
Il dataset contiene informazioni aggregate sui voli in arrivo, incluse cause dei ritardi, numero di voli, cancellazioni e deviazioni.  
Prima dell’analisi, i dati sono stati puliti (rimozione dei valori mancanti) e campionati dove necessario per migliorare leggibilità e performance.

---

## Grafici e Analisi

### 1. Distribuzione dei Ritardi di Arrivo
- **Grafico:** Istogramma  
- **Titolo:** Distribution of Arrival Delays  
- **Descrizione:** Mostra la frequenza dei ritardi di arrivo in minuti. La maggior parte dei voli ha ritardi bassi (vicino a 0), con una rapida decrescita per ritardi più alti.  
- **Utilità:** Permette di capire la distribuzione generale dei ritardi e individuare eventuali anomalie.

---

### 2. Scatter Plot – Voli vs Ritardi
- **Grafico:** Scatter plot campionato  
- **Titolo:** Arriving Flights vs Arrival Delay  
- **Descrizione:** Visualizza la relazione tra numero di voli in arrivo e ritardo medio. I dati mostrano forte concentrazione nei voli con basso traffico, con ritardi variabili fino a 600 minuti.  
- **Utilità:** Analizza se esiste correlazione tra traffico aereo e ritardi.

---

### 3. Hexbin Plot – Densità Voli vs Ritardi
- **Grafico:** Hexbin con scala logaritmica  
- **Titolo:** Density of Arrival Delay vs Flights  
- **Descrizione:** Mappa di densità che evidenzia le aree con maggiore concentrazione di dati. Celle rosse scure indicano dove si verificano più ritardi.  
- **Utilità:** Evita sovrapposizione di punti e mostra chiaramente le zone critiche.

---

### 4. Hexbin con Asse Logaritmico
- **Grafico:** Hexbin con logaritmo su arr_flights  
- **Titolo:** Density of Arrival Delay vs log  
- **Descrizione:** Trasformazione logaritmica sul numero di voli per espandere la zona densa e migliorare leggibilità.  
- **Utilità:** Rende visibili pattern nascosti nelle fasce basse di traffico.

---

### 5. Ritardo Medio per Mese
- **Grafico:** Line plot  
- **Titolo:** Average Arrival Delay by Month  
- **Descrizione:** Mostra l’andamento mensile del ritardo medio. Picchi nei mesi di febbraio (2) e dicembre (12), minimo in aprile (4).  
- **Utilità:** Analizza la stagionalità dei ritardi e supporta la pianificazione operativa.

---

### 6. Boxplot per Compagnia Aerea
- **Grafico:** Boxplot  
- **Titolo:** Arrival Delay Distribution by Carrier  
- **Descrizione:** Confronta la distribuzione dei ritardi tra compagnie aeree. Ogni box mostra mediana, quartili e outlier.  
- **Utilità:** Identifica le compagnie più soggette a ritardi e confronta la loro performance.

---

### 7. Heatmap delle Correlazioni
- **Grafico:** Heatmap  
- **Titolo:** Correlation Matrix with Values  
- **Descrizione:** Visualizza le correlazioni tra variabili numeriche: ritardi, cause, numero di voli, cancellazioni, ecc. Celle scure indicano correlazioni forti.  
- **Utilità:** Aiuta a capire quali fattori influenzano maggiormente i ritardi.

---

## Conclusioni
I grafici offrono una panoramica completa e visivamente efficace dei ritardi aerei. Permettono di:
- Individuare pattern stagionali  
- Confrontare compagnie aeree  
- Analizzare l’impatto del traffico sui ritardi  
- Esplorare le cause principali dei ritardi  

Questo progetto fornisce informazioni utili per migliorare la gestione operativa dei voli e ridurre i ritardi.



# Analisi e Modelli di Ritardo dei Voli

## Descrizione del Progetto
Questo progetto analizza i ritardi dei voli negli Stati Uniti usando dati aggregati sulle cause principali dei ritardi:
- `carrier_delay` (ritardo del vettore)
- `weather_delay` (ritardo meteorologico)
- `nas_delay` (ritardo dovuto al National Air System)
- `security_delay` (ritardo dovuto a controlli di sicurezza)
- `late_aircraft_delay` (ritardo dovuto a arrivi tardivi di aerei)

Viene effettuata un’analisi esplorativa dei dati, seguita dalla costruzione di modelli di regressione con **XGBoost** e **LightGBM** per predire i ritardi in minuti.  

## Struttura del Dataset
- **Features** principali:
  - `month`: mese del volo
  - `arr_flights`: numero di voli in arrivo
  - `arr_del15`: numero di voli con ritardo > 15 min
  - `arr_cancelled`: numero di voli cancellati
  - `arr_diverted`: numero di voli dirottati
- **Target**: ritardi in minuti per le diverse cause.

Il dataset è stato pulito rimuovendo valori mancanti (`dropna()`).

## Analisi Esplorativa
- Matrici di correlazione tra le variabili numeriche.
- Scatter plot tra `arr_flights` e `arr_delay` per identificare pattern nei ritardi.
- Grafici a barre per confrontare RMSE e R² dei modelli su ciascuna causa di ritardo.

## Modelli
- **XGBoost**: Regressore per stimare i ritardi.  
- **LightGBM**: Regressore alternativo per confrontare performance.  

### Metriche di Valutazione
- RMSE (Root Mean Squared Error) in minuti.  
- R² per misurare quanto il modello spiega la varianza del target.  

I risultati mostrano quale modello è più accurato per ciascuna causa di ritardo.

## Risultati
- Grafici comparativi di RMSE e R² tra XGBoost e LightGBM.
- Insight: alcuni ritardi (come `nas_delay` o `late_aircraft_delay`) sono meglio predetti rispetto ad altri (`security_delay`).

## Come Usare
1. Installare le librerie richieste:
   ```bash
   pip install pandas numpy matplotlib seaborn scikit-learn xgboost lightgbm
