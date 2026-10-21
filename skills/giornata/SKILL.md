---
name: giornata
description: Riepilogo della giornata in AraWeb CRM. Usala quando l'utente saluta a inizio giornata o chiede «com'è la giornata», «cosa c'è oggi», «chi viene stasera», «cosa devo fare oggi», «fammi il punto», o vuole sapere prenotazioni, cose da fare e clienti da richiamare.
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

**Cose da fare** — prima quelle scadute, poi quelle di oggi; delle altre di' solo quante sono.

**In uscita oggi** — contenuti del calendario editoriale con ora e canale, e il loro stato se non sono ancora approvati.

**Da richiamare** — al massimo cinque clienti abituali in ritardo, con nome e telefono. Se sono di più, dillo e proponi una lista salvata.

Se `riepilogo` dice `sola_lettura: true`, apri il riepilogo avvisando che l'abbonamento è scaduto e il gestionale è in sola lettura.

## 4. Chiudi con al massimo due proposte
Scegli le azioni più utili tra quelle che i dati suggeriscono, per esempio «Vuoi che segni come confermata la prenotazione di Sara?» o «Preparo un messaggio per i clienti in ritardo?». Eseguile solo dopo il sì dell'utente, con `aggiorna_appuntamento`, `segna_cosa_da_fare` o la skill `promozioni`.

## Da non fare
- Non mostrare id, campi tecnici o JSON.
- Non inventare dati che gli strumenti non hanno restituito: se una chiamata fallisce, dillo in una riga e continua con il resto.
