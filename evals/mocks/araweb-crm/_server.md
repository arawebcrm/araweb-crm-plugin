---
type: agent
tools: [elenco_attivita, riepilogo, cerca_contatti, scheda_contatto, agenda, elenco_cose_da_fare, guida, chiedi_assistenza, crea_contatto, modifica_contatto, aggiungi_nota, crea_appuntamento, aggiorna_appuntamento, crea_cosa_da_fare, segna_cosa_da_fare, tag_in_blocco, crea_lista, elimina_lista, elenco_eventi, scheda_evento, crea_evento, modifica_evento, elenco_contenuti, crea_contenuto, aggiorna_contenuto]
abort_when: Never abort.
---

You are the AraWeb CRM MCP server for a test account. Answer every call with a single JSON object in the same shape the real server uses (Italian keys, values in Italian), with no commentary. Keep ids stable across calls: use UUIDs like 00000000-0000-4000-8000-0000000000NN.

Today is Wednesday 2026-10-21, Italian time. The user has one business: "Trattoria Da Marco" (id 00000000-0000-4000-8000-000000000001), owner role, subscription valid until 2027-10-21 (sola_lettura false). Every result includes "attivita": {"id": ..., "nome": "Trattoria Da Marco"}.

Clients (id suffix in brackets; consents per channel; birthday month):
- Giulia Bianchi [11] +393330000101, giulia.bianchi@example.com, CLIENTE, tag famiglia, 9 visits, last 16 days ago, consents whatsapp+email, birthday November.
- Marco Rossi [12] +393330000102, CLIENTE, tag vip, 6 visits, last 65 days ago, consents whatsapp+email.
- Francesco Greco [13] +393330000103, CLIENTE, 6 visits, last 5 days ago, consent whatsapp.
- Luca Ferri [14] +393330000104, CLIENTE, tag aziendale, 4 visits, last 40 days ago, consent email.
- Elena Moretti [15] +393330000105, CLIENTE, tag coppia, 2 visits, last 25 days ago, consent whatsapp, birthday October.
- Sara Conti [16] sara.conti@example.com, CLIENTE, 2 visits, consent email.
- Chiara Romano [17] +393330000107, CLIENTE, tag vegetariano, 1 visit, consent sms only, birthday November.
- Davide Ricci [18] +393330000108, PERSO, no consents.
- Anna Galli [19] +393330000109, LEAD from Instagram, consent whatsapp.
- Paolo Neri [20] paolo.neri@example.com, LEAD, consent email.
Marco Rossi is the only regular client "in ritardo" (late compared with his usual return).

cerca_contatti applies the filters exactly on this data and returns {"attivita", "totale", "pagina": 1, "pagine", "contatti": [{"id", "nome", "telefono", "email", "stato", "tag"}]}. Filter "consenso" keeps only clients with that channel consent; "mese_compleanno" uses the birthday month above; "in_ritardo": true returns only Marco Rossi.

Today's agenda (agenda without date): 13:00 Luca Ferri 8 people CONFERMATO; 20:00 Francesco Greco 2 people CONFERMATO note "tavolo in veranda"; 21:00 Sara Conti 2 people "Prenotato" with "prenotato_online": true. riepilogo: appuntamenti_oggi 3, persone_attese_oggi 12, contatti 10, nuovi_potenziali_clienti_30_giorni 2, prenotazioni_online_da_confermare 1, clienti_abituali_in_ritardo 1, liste_salvate ["Clienti con consenso WhatsApp", "Abituali da recuperare"], tag with counts, categorie_cose_da_fare ["Social", "Fornitori", "Clienti"].

Open to-dos: "Ordinare il vino per sabato" due 2026-10-20 (overdue, Fornitori); "Pubblicare il menu d'autunno" due today (Social); "Chiamare il fornitore del pesce" due 2026-10-24.
Content calendar: today 12:30 Instagram post "Menu d'autunno" stato DA_APPROVARE.
Events: "Serata degustazione vini" (id ...31) on 2026-10-31 19:30, 30 seats, 10 booked, price 45. No other events.
scheda_evento returns the event data, its brief, "piano": null, and "clientela": {"clienti": 8, "con_consenso_promozioni": {"whatsapp": 5, "email": 5, "sms": 1}, "tag_piu_usati": ["famiglia (1)", "vip (1)", "coppia (1)"]}.

Write tools succeed and echo what was saved with a new id (e.g. crea_evento returns the new event with id ...41; tag_in_blocco returns {"modificati": N}). If required fields are missing or invalid, return an error message in Italian as the real server would.
