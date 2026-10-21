---
name: recupero-clienti
description: Far tornare i clienti che non vengono da un po' con AraWeb CRM: chi è in ritardo rispetto al suo solito, chi manca da mesi, i clienti abituali persi di vista. Usala quando l'utente dice «i clienti non tornano», «chi non viene più», «ci mancano i clienti di una volta», vuole una campagna per riportarli, o chiede com'è andato un recupero già fatto.
---

# Recupero dei clienti

Una piccola sequenza di messaggi, al massimo tre in tre settimane, ai clienti che venivano e non vengono più, solo a chi ha dato il consenso per quel canale. Il gestionale non manda messaggi: tu prepari destinatari, testi e promemoria, l'utente li invia.

## 1. Chi recuperare
Se non sai su quale attività lavorare, chiama `elenco_attivita`, poi `riepilogo` per sapere quanti clienti abituali sono in ritardo. Chiedi il canale (whatsapp, email o sms) se non l'ha detto.

Scegli il gruppo con `cerca_contatti`, sempre con `consenso` uguale al canale e `stato: "CLIENTE"`:
- **abituali in ritardo** (il gruppo migliore): `in_ritardo: true`;
- **spariti da mesi**: `ultima_visita: "oltre90"` (o `oltre180`) con `numero_visite: "2"`, così escludi chi è venuto una volta sola.

Mostra il totale e i primi nomi, e chiedi conferma. Se nessuno ha il consenso per quel canale, dillo e proponi un altro canale: mai scrivere a chi non ha il consenso. Lascia fuori i contatti segnati come persi: di solito hanno un motivo (si sono trasferiti, hanno chiesto di non essere contattati).

## 2. La sequenza
Chiedi all'utente se può offrire un piccolo incentivo (un dolce, un calice, uno sconto) e fino a quando: non inventarlo. Poi proponi:
1. **Subito – «Ci manchi»**: tono da persona, una novità concreta (menu, piatto, orari) e l'invito a tornare.
2. **Dopo 7–10 giorni, solo a chi non è ancora tornato – l'incentivo**: chiaro, con la scadenza.
3. **Dopo altre 2 settimane, facoltativo – il parere**: una domanda semplice («c'è qualcosa che possiamo fare meglio?»), senza insistere.

Ogni messaggio: nome dell'attività, `{nome}` del cliente, una sola richiesta e come non ricevere più messaggi («Rispondi STOP…»). Per lunghezza e tono segui la skill `formati-canali`. Mai più di un messaggio a settimana alla stessa persona.

## 3. Per seguire chi torna
Dopo il sì dell'utente:
- `tag_in_blocco` con gli stessi filtri del punto 1 e un tag tipo `recupero-ottobre-2026`;
- `crea_lista` «Recupero ottobre 2026 – non ancora tornati» con `tag` uguale al tag e `ultima_visita: "oltre30"`: è la lista da usare per il secondo e il terzo messaggio, perché chi torna ne esce da solo;
- `crea_cosa_da_fare` per il giorno del secondo e del terzo invio, con il nome della lista nelle note.

Per WhatsApp ricorda in una riga di usare una lista broadcast di WhatsApp Business e non tanti messaggi uguali uno per uno.

## 4. Com'è andata
Quando l'utente lo chiede (dopo 2–4 settimane): `cerca_contatti` con il `tag` del recupero, poi con lo stesso tag e `ultima_visita: "entro30"`. Rispondi con quanti erano, quanti sono tornati e la percentuale, i nomi di chi è tornato e un consiglio pratico per la prossima volta.

## Cosa consegnare
1. **Destinatari**: canale, filtri e quanti sono.
2. **I messaggi** pronti da copiare, con il giorno di invio.
3. **Come seguirli**: tag, lista e promemoria proposti.
