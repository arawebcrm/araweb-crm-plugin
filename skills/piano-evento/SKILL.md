---
name: piano-evento
description: Organizza un evento aperto al pubblico in AraWeb CRM e il suo piano di comunicazione (Cenone di Capodanno, serata degustazione, festa, saldi, open day). Usala quando l'utente vuole creare un evento, riempire i posti, preparare post e messaggi per promuoverlo, mettere in ordine scadenze e calendario editoriale di un evento, o capire se le prenotazioni stanno andando bene.
---

# Piano per un evento

Risultato: l'evento nel gestionale con brief e piano salvati, le scadenze e i controlli come cose da fare e i contenuti in bozza nel calendario editoriale. Prima mostri il piano, poi scrivi nel gestionale solo dopo il sì dell'utente.

## 1. Trova o crea l'evento
Se non sai su quale attività lavorare, chiama `elenco_attivita`. Poi `elenco_eventi`: se l'evento c'è già, usa il suo id. Se è nuovo, ti servono nome e inizio; chiedi in un solo messaggio posti, prezzo a persona, a chi si rivolge e l'obiettivo, se non li ha detti. Crealo con `crea_evento` solo dopo la conferma dell'utente.

## 2. Leggi la scheda
Chiama `scheda_evento`. Guarda posti liberi, prenotazioni, brief già scritto, eventuale piano esistente e i numeri della clientela: quanti clienti, quanti con consenso per canale, tag più usati. Se c'è già un piano, chiedi se aggiornarlo o rifarlo.

## 3. Prepara il piano
Scrivilo in italiano semplice, breve, in questo ordine:
1. **Obiettivo in numeri**: posti da riempire e, se ha senso, clienti nuovi. Aggiungi due soglie di controllo, per esempio «metà dei posti a 14 giorni, tre quarti a 7 giorni».
2. **A chi parliamo** e **messaggio chiave** in una frase.
3. **Canali**: usa solo quelli che hanno senso con i numeri della scheda. WhatsApp, email e SMS solo se ci sono clienti con quel consenso, e dillo con il numero (es. «WhatsApp: 120 clienti con consenso»).
4. **Calendario a ritroso** dalla data dell'evento: lancio, promemoria, ultimi posti, giorno prima, giorno stesso. Conta i tempi di preparazione prima di ogni uscita: foto e grafica 2 giorni, volantini da stampare 5 giorni, menu o programma definitivo prima del lancio. Per eventi entro due settimane comprimi i tempi. Nessuna data nel passato.
5. **Budget**, se c'è, diviso per canale.
6. **Cose da preparare**: menu o programma, ordini ai fornitori, stampa volantini, personale.
7. **Se le prenotazioni vanno piano**: al massimo tre rischi con il rimedio già deciso (es. «a 7 giorni meno di metà dei posti: secondo messaggio WhatsApp ai clienti con consenso e una storia con il conto alla rovescia»).
8. **Dopo l'evento**: il giorno dopo un grazie con la richiesta di recensione a chi è venuto, e un breve parere; se è andata bene, «ci vediamo al prossimo».

Mostra il piano e chiedi conferma. Se i posti sono già quasi finiti, proponi meno promozione e una lista d'attesa.

## 4. Salva nel gestionale
Dopo il sì, in quest'ordine:
- `modifica_evento` con `piano` (il testo del piano) e i campi del brief che erano vuoti: `pubblico`, `obiettivo`, `punti_di_forza`, `canali`, `budget_euro`.
- `crea_cosa_da_fare` con `evento_id` per ogni preparativo interno, con la sua scadenza, e una per ogni soglia di controllo (es. «Controllare le prenotazioni: obiettivo 40 posti»).
- `crea_contenuto` con `evento_id` per ogni post, storia, reel, email o messaggio del calendario, compreso il grazie del giorno dopo. Scrivi testo e grafica seguendo la skill `formati-canali`. Stato `BOZZA`; `APPROVATO` solo se l'utente lo chiede esplicitamente.

I messaggi diretti ai clienti (WhatsApp, email, SMS) seguono le regole della skill `promozioni`: solo a chi ha il consenso per quel canale, con mittente e modo di disiscriversi nel testo. Per il grazie del giorno dopo i destinatari sono quelli di `cerca_contatti` con `evento` e `solo_presenti: true`.

## 5. Chiudi
Riassumi cosa hai creato (quante cose da fare, quanti contenuti) e dove trovarli nel gestionale: **Marketing → Eventi**, **Marketing → Calendario editoriale** e la pagina **Attività**. Se l'evento accetta prenotazioni online, ricorda che link e QR sono nella scheda dell'evento.

## Come sta andando
Se l'utente chiede a che punto è un evento, leggi `scheda_evento` e confronta le prenotazioni con l'obiettivo e con la soglia del giorno. Se è sotto, proponi il rimedio previsto nel piano; se l'evento è passato, di' quanti sono venuti rispetto ai prenotati e proponi il grazie con la recensione.
