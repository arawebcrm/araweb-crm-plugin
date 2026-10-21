---
name: piano-evento
description: Organizza un evento aperto al pubblico in AraWeb CRM e il suo piano di comunicazione (Cenone di Capodanno, serata degustazione, festa, saldi, open day). Usala quando l'utente vuole creare un evento, riempire i posti, preparare post e messaggi per promuoverlo o mettere in ordine scadenze e calendario editoriale di un evento.
---

# Piano per un evento

Risultato: l'evento nel gestionale con brief e piano salvati, le scadenze come cose da fare e i contenuti in bozza nel calendario editoriale. Prima mostri il piano, poi scrivi nel gestionale solo dopo il sì dell'utente.

## 1. Trova o crea l'evento
Se non sai su quale attività lavorare, chiama `elenco_attivita`. Poi `elenco_eventi`: se l'evento c'è già, usa il suo id. Se è nuovo, ti servono nome e inizio; chiedi in un solo messaggio posti, prezzo a persona, a chi si rivolge e l'obiettivo, se non li ha detti. Crealo con `crea_evento` solo dopo la conferma dell'utente.

## 2. Leggi la scheda
Chiama `scheda_evento`. Guarda posti liberi, prenotazioni, brief già scritto, eventuale piano esistente e i numeri della clientela: quanti clienti, quanti con consenso per canale, tag più usati. Se c'è già un piano, chiedi se aggiornarlo o rifarlo.

## 3. Prepara il piano
Scrivilo in italiano semplice, breve, in questo ordine:
1. **Obiettivo in numeri**: posti da riempire, clienti nuovi.
2. **A chi parliamo** e **messaggio chiave** in una frase.
3. **Canali**: usa solo quelli che hanno senso con i numeri della scheda. WhatsApp, email e SMS solo se ci sono clienti con quel consenso, e dillo con il numero (es. «WhatsApp: 120 clienti con consenso»).
4. **Calendario a ritroso** dalla data dell'evento: lancio, promemoria, ultimi posti, giorno prima, giorno stesso, ringraziamento e richiesta di recensione il giorno dopo. Per eventi entro due settimane comprimi i tempi. Nessuna data nel passato.
5. **Budget**, se c'è, diviso per canale.
6. **Cose da preparare**: menu o programma, ordini ai fornitori, stampa volantini, personale.

Mostra il piano e chiedi conferma. Se i posti sono già quasi finiti, proponi meno promozione e una lista d'attesa.

## 4. Salva nel gestionale
Dopo il sì, in quest'ordine:
- `modifica_evento` con `piano` (il testo del piano) e i campi del brief che erano vuoti: `pubblico`, `obiettivo`, `punti_di_forza`, `canali`, `budget_euro`.
- `crea_cosa_da_fare` con `evento_id` per ogni preparativo interno, con la sua scadenza.
- `crea_contenuto` con `evento_id` per ogni post, storia, reel, email o messaggio del calendario: `canale`, `uscita` in ora italiana (AAAA-MM-GGTHH:MM), `titolo`, `testo` pronto e `grafica` con cosa deve mostrare la foto. Stato `BOZZA`; `APPROVATO` solo se l'utente lo chiede esplicitamente.

I messaggi diretti ai clienti (WhatsApp, email, SMS) seguono le regole della skill `promozioni`: solo a chi ha il consenso per quel canale, con mittente e modo di disiscriversi nel testo.

## 5. Chiudi
Riassumi cosa hai creato (quante cose da fare, quanti contenuti) e dove trovarli nel gestionale: **Marketing → Eventi**, **Marketing → Calendario editoriale** e la pagina **Attività**. Se l'evento accetta prenotazioni online, ricorda che link e QR sono nella scheda dell'evento.
