---
name: formati-canali
description: Come scrivere post Instagram, storie, reel, post Facebook e TikTok, newsletter, messaggi WhatsApp, post su Google e volantini per un ristorante, un negozio o un'attività locale, e come metterli nel calendario editoriale di AraWeb CRM. Usala quando l'utente chiede di scrivere un contenuto per i social o per i clienti, o quando un'altra skill prepara i testi di un piano.
---

# Formati dei canali

Testi per un'attività locale: concreti, brevi, in italiano parlato. Ogni contenuto dice **cosa**, **quando**, **quanto costa** (se serve) e **come prenotare o venire**, con un solo invito all'azione.

## Regole per tutti i canali
- Apri con il dettaglio più concreto (il piatto, il vino, lo sconto, la data), non con un saluto generico.
- Niente parole vuote come «imperdibile», «esperienza unica», «eccellenza»: meglio un dettaglio vero («il produttore racconta i suoi cinque vini»).
- Prezzi e date sempre scritti per intero («venerdì 31 ottobre, ore 19:30, 45 € a persona»).
- Al massimo due emoji, mai al posto delle parole.
- Niente riferimenti a salute, allergie o diete, e niente promesse che l'utente non ha fatto.

## Canale per canale
Il nome a sinistra è il valore di `canale` in `crea_contenuto`.

| Canale | Testo | Cosa mostrare (`grafica`) |
|---|---|---|
| `instagram_post` | Gancio nella prima riga (si vede prima del «altro»), poi 3–5 righe; chiudi con come prenotare («Prenota in DM o chiamaci»; il numero solo se l'utente l'ha dato). 3–5 hashtag della città e del tema in fondo. | Una foto vera e luminosa del piatto, del locale o delle persone; testo sulla foto solo per data e prezzo. |
| `instagram_storia` | Una frase sola, grande; usa sticker (sondaggio, conto alla rovescia, link). Le storie di una sequenza vanno in contenuti separati. | Verticale 9:16, primo piano; cosa scrivere nello sticker. |
| `reel` | Testo in sovrimpressione di 3–6 parole per scena e una didascalia breve come il post. | 3–5 scene da 2–3 secondi (preparazione, piatto finito, sala piena); musica di tendenza. |
| `facebook` | Come il post Instagram ma con più dettagli pratici (indirizzo, parcheggio, orari); niente muro di hashtag. | La stessa foto del post. |
| `tiktok` | Gancio parlato nei primi 2 secondi; didascalia di una riga. | Video verticale girato col telefono, dietro le quinte. |
| `email` | Oggetto fino a 50 caratteri con il dettaglio concreto; anteprima di una riga; corpo con 3 paragrafi brevi e un pulsante o link. In fondo come disiscriversi. | Una foto in alto. |
| `whatsapp` | 4–5 righe, tono da persona, `{nome}` per il nome del cliente, nome dell'attività e «Rispondi STOP se non vuoi più ricevere le nostre offerte». Solo a chi ha il consenso WhatsApp (skill `promozioni`). | Facoltativa: una foto. |
| `google` | Post del profilo dell'attività su Google: 2–3 frasi con data e cosa c'è, pulsante «Prenota» o «Chiama». | Foto orizzontale del locale o del piatto. |
| `volantino` | Titolo di 3–5 parole, data e ora grandi, prezzo, 3 punti su cosa è incluso, telefono e indirizzo, QR della prenotazione online se c'è. | Formato A5, una foto, colori del locale. |

## Orari di uscita
Per un ristorante: post e storie tra le 11:30 e le 12:30 o tra le 18:00 e le 19:30; newsletter e WhatsApp a metà mattina. Per un negozio: metà mattina o tardo pomeriggio. Mai di notte. Gli orari vanno in ora italiana, formato `AAAA-MM-GGTHH:MM`.

## Nel calendario editoriale
Con `crea_contenuto`: `titolo` corto che dica cos'è («Annuncio serata degustazione»), `testo` pronto da copiare, `grafica` con le indicazioni della colonna a destra, `evento_id` se il contenuto è per un evento. Stato `BOZZA` (o `DA_APPROVARE` se l'utente vuole farlo vedere a qualcuno); `APPROVATO` solo se l'utente lo chiede. Un contenuto per ogni uscita: post e storia dello stesso giorno sono due contenuti.
