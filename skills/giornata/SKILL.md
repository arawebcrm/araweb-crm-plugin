---
name: giornata
description: Riepilogo della giornata in AraWeb CRM. Usala quando l'utente saluta a inizio giornata o chiede «com'è la giornata», «cosa c'è oggi», «chi viene stasera», «cosa devo fare oggi», «fammi il punto», o vuole sapere prenotazioni, cose da fare e clienti da richiamare. Usala anche per le scadenze dei clienti di un consulente o di uno studio (disinfestazioni, piani HACCP, formazione) e per fissarne gli interventi.
---

# Il giro della giornata

Obiettivo: in meno di un minuto di lettura, l'utente sa chi arriva oggi, cosa deve confermare o fare e chi vale la pena richiamare. Solo lettura: non cambiare nulla senza che l'utente lo chieda.

## 1. Quale attività
Se non sai su quale attività lavorare, chiama `elenco_attivita`. Con più attività e nessuna indicazione, fai il giro di ciascuna (al massimo tre), una sezione per attività con il suo nome come titolo.

## 2. Raccogli i dati
Chiama, per l'attività scelta:
- `riepilogo`: numeri di oggi, prenotazioni online da confermare, clienti abituali in ritardo, abbonamento.
- `agenda` senza data (è oggi).
- `elenco_cose_da_fare`.
- `elenco_contenuti` con `giorni: 1`, per i post e i messaggi in uscita oggi.
- Solo se `clienti_abituali_in_ritardo` è più di zero: `cerca_contatti` con `in_ritardo: true`.

## 3. Scrivi il riepilogo
Usa questo ordine e salta le sezioni vuote. Frasi brevi, niente tabelle lunghe, orari in ora italiana (20:30).

**Oggi** — quanti appuntamenti e quante persone attese, poi l'elenco: ora, nome, persone, e le note utili al servizio (tavolo preferito, ricorrenza). Segna gli eventi interni e le prenotazioni per un evento.

**Da confermare** — le prenotazioni online ancora da confermare (in `agenda` hanno `prenotato_online: true` e stato «Prenotato»), con il telefono per chiamare.

**Cose da fare** — prima quelle scadute, poi quelle di oggi; delle altre di' solo quante sono. Per ognuna, se ci sono: con chi è condivisa (`persone`: possono esserci anche collaboratori senza account, per esempio una ditta esterna), ogni quanto si ripete (`si_ripete`, già in parole: «ogni 6 mesi», «il primo lunedì del mese»), l'intervento già fissato (`intervento`, con la data) e i passi della checklist spuntati (`passi`, es. «3/5»).

**In uscita oggi** — contenuti del calendario editoriale con ora e canale, e il loro stato se non sono ancora approvati.

**Da richiamare** — al massimo cinque clienti abituali in ritardo, con nome e telefono. Se sono di più, dillo e proponi una lista salvata.

Se `riepilogo` dice `sola_lettura: true`, apri il riepilogo avvisando che l'abbonamento è scaduto e il gestionale è in sola lettura.

## 4. Chiudi con al massimo due proposte
Scegli le azioni più utili tra quelle che i dati suggeriscono, per esempio «Vuoi che segni come confermata la prenotazione di Sara?» o «Preparo un messaggio per i clienti in ritardo?». Eseguile solo dopo il sì dell'utente, con `aggiorna_appuntamento`, `segna_cosa_da_fare`, `crea_appuntamento` (per fissare un intervento, vedi sotto) o la skill `promozioni`.

## 5. Scadenze dei clienti e interventi (consulenti e studi)
- Le scadenze di un'azienda sono quelle dei suoi referenti: trovi i referenti con `cerca_contatti` e in `elenco_cose_da_fare` le riconosci dal `contatto`. Una scadenza nuova per un'azienda si crea con `crea_cosa_da_fare` e il `contatto_id` del referente.
- Una scadenza che si ripete si crea con `ripeti_ogni_mesi` (6 = due volte l'anno, 12 = ogni anno, 36 = ogni 3 anni); `ripeti_ogni_giorni` per «ogni 15 giorni» o «ogni 2 settimane» (da 7 a 364, non insieme ai mesi); un giorno fisso come «il primo lunedì del mese» con `ripeti_ogni_mesi` più `ripeti_settimana_del_mese` (1–4, o -1 per l'ultimo) e `ripeti_giorno_settimana` (1 = lunedì … 7 = domenica). Se la data indicata non cade nella regola, la prima scadenza viene portata alla prima volta che cade: dillo all'utente. Per darla anche ad altri usa `persone` con i nomi di chi ha accesso all'attività. `avvisa_cliente` manda al referente un WhatsApp 15 giorni prima, solo se ha dato il consenso e mai con le ripetizioni a giorni: non prometterlo a chi non ce l'ha.
- Il `riepilogo` elenca i tipi di intervento (le categorie) con le loro voci di catalogo (titolo e ripetizione). Se l'utente nomina un servizio del catalogo («la disinfestazione», «il controllo delle esche»), crea la scadenza con quel titolo, la sua categoria e la sua ripetizione invece di inventarne una; se non c'è una voce adatta, titolo libero. Le categorie archiviate non compaiono.
- Le note di un cliente (il diario dell'azienda) si scrivono con `aggiungi_nota` e `azienda_id` al posto di `contatto_id`, con al massimo 5 tag brevi (sopralluogo, preventivo, reclamo). L'id dell'azienda è in `scheda_contatto` di un suo referente (`azienda.id`), che mostra anche la nota «In evidenza» e le ultime 5 note. Un'azienda senza referenti non si raggiunge: la nota si scrive dal gestionale. Le leggono tutte le persone dello studio: mai dati sulla salute. Con `contatto_id` resta la cronologia del referente.
- Per fissare la data di una scadenza usa `crea_appuntamento` con `cosa_da_fare_id` (il cliente è il referente: non indicarne un altro). Quando l'appuntamento è segnato arrivato con `aggiorna_appuntamento`, la cosa da fare diventa fatta e, se si ripete, nasce la successiva: di' all'utente la data della prossima. Riportare indietro l'appuntamento non riapre la cosa da fare.
- Se segui più clienti come agenzia e hanno il modulo Autocontrollo, puoi leggere i loro registri con `autocontrollo_stato` su ciascuna attività (vedi la skill `autocontrollo`). Un cliente che ti ha dato solo l'Autocontrollo («Solo Autocontrollo») non compare in `elenco_attivita` e non si può scegliere: i suoi registri si aprono dal gestionale.

## Da non fare
- Non mostrare id, campi tecnici o JSON.
- Non inventare dati che gli strumenti non hanno restituito: se una chiamata fallisce, dillo in una riga e continua con il resto.
- Non assegnare una scadenza a un collaboratore senza account per nome e non spuntare né scrivere i passi di una checklist: non ci sono strumenti, si fa dal gestionale (Collaboratori e il dettaglio della scadenza). Segnare fatta una scadenza con passi ancora aperti si può, e la risposta lo dice («2 passi su 5 non sono spuntati»): riportalo all'utente.
- Non ci sono strumenti per i documenti delle aziende e per l'area download dei clienti (modulo Consulenza): si caricano, si leggono e si mandano solo dalla scheda dell'azienda nel gestionale. Dillo, e non chiedere all'utente di incollare il contenuto di un documento del cliente.
