---
name: promozioni
description: Prepara promozioni e messaggi ai clienti con AraWeb CRM (WhatsApp, email, SMS) scegliendo i destinatari solo tra chi ha dato il consenso. Usala per auguri di compleanno, offerte, inviti a un evento, recupero dei clienti che non vengono da tempo, newsletter, o quando l'utente chiede «a chi posso scrivere» o «prepara un messaggio per i clienti».
---

# Promozioni ai clienti

Il gestionale non manda messaggi: tu prepari destinatari e testo, l'utente li invia dal suo WhatsApp, dalla sua email o dal suo programma di newsletter. Le regole sul consenso non hanno eccezioni.

## 1. Chiarisci la richiesta
Ti servono: **canale** (whatsapp, email o sms), **occasione** e **a chi** (compleanni del mese, chi non viene da tempo, chi ha prenotato un evento, un tag, una lista salvata). Se manca il canale, chiedilo: un messaggio vale per un solo canale. Se non sai su quale attività lavorare, chiama `elenco_attivita`.

## 2. Trova i destinatari
Chiama `cerca_contatti` sempre con `consenso` uguale al canale, più i filtri dell'occasione:
- compleanni: `mese_compleanno`
- chi non viene da tempo: `ultima_visita` (es. `oltre90`) oppure `in_ritardo: true` per gli abituali
- clienti fedeli: `numero_visite` (es. `5`)
- un evento: `evento` con l'id da `elenco_eventi` (per i ringraziamenti, anche `solo_presenti: true`)
- un gruppo già usato: `tag` o `lista` (i nomi sono in `riepilogo`)

Mostra il `totale` e i primi nomi, poi chiedi conferma prima di proseguire. Se il totale è zero, dillo e proponi filtri meno stretti o un altro canale: non proporre mai di scrivere a chi non ha il consenso per quel canale, nemmeno «solo questa volta». Il consenso email non vale per WhatsApp.

## 3. Scrivi il testo
Prendi il nome dell'attività dal risultato degli strumenti e mettilo sempre nel testo, insieme al modo per non ricevere più messaggi.
- **WhatsApp**: massimo 4-5 righe, tono da persona, `{nome}` dove va il nome del cliente, al massimo un'emoji. Chiudi con «Rispondi STOP se non vuoi più ricevere le nostre offerte».
- **Email**: oggetto (massimo 50 caratteri) e corpo breve con un solo invito all'azione. Chiudi con il modo per disiscriversi (es. «Per non ricevere più queste email rispondi CANCELLAMI»).
- **SMS**: massimo 160 caratteri, nome dell'attività in apertura, «STOP» per disiscriversi.

Niente urgenza finta, niente promesse che l'utente non ha fatto, niente riferimenti a salute, allergie o diete. Proponi una sola versione; ne scrivi altre solo se l'utente le chiede.

## 4. Dopo il testo
Proponi, ed esegui solo dopo il sì dell'utente:
- un **tag** su chi riceve il messaggio, con `tag_in_blocco` e gli stessi filtri del punto 2, nome tipo `promo-capodanno-2026`: così dopo si sa a chi è arrivato;
- una **lista salvata** con `crea_lista` se la stessa ricerca servirà ancora (es. «Compleanni con WhatsApp»).

Per WhatsApp ricorda in una riga che tanti messaggi uguali mandati uno per uno dal numero normale possono far bloccare il numero: con WhatsApp Business conviene una lista broadcast.

## Cosa consegnare
1. **Destinatari**: canale, filtri usati e quanti sono.
2. **Testo** pronto da copiare.
3. **Prossimi passi**: tag o lista proposti, e come inviarlo.

## Da non fare
- Non cambiare i consensi e non aggiungere persone a mano all'elenco dei destinatari.
- Non esportare elenchi di numeri o email nella chat: l'utente li trova nel gestionale in Contatti, con gli stessi filtri o con la lista salvata.
