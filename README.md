# AraWeb CRM per Claude

Plugin ufficiale di [AraWeb CRM](https://crm.araweb.cloud), il gestionale dei clienti per ristoranti, negozi e altre attività. Collega Claude al tuo gestionale e gli insegna a fare bene tre lavori di tutti i giorni, con i tuoi stessi permessi.

## Cosa contiene

- **Connettore AraWeb CRM** (`https://crm.araweb.cloud/mcp`): gli strumenti per leggere e aggiornare contatti, agenda, cose da fare, eventi e calendario editoriale. È lo stesso connettore della directory di Claude: se lo hai già collegato, non lo vedi doppio.
- **Skill `giornata`**: il giro del mattino. Appuntamenti di oggi, prenotazioni online da confermare, cose da fare in scadenza, contenuti in uscita e clienti abituali da richiamare, in un riassunto breve.
- **Skill `promozioni`**: dal «prepara gli auguri per chi compie gli anni a novembre» al testo pronto, scegliendo i destinatari solo tra chi ha dato il consenso per quel canale, con mittente e modo di disiscriversi nel testo e un tag per ricordare chi l'ha ricevuto.
- **Skill `piano-evento`**: dalla scheda di un evento (Cenone di Capodanno, serata degustazione, saldi) al piano di comunicazione salvato nel gestionale, con le cose da fare e i contenuti in bozza nel calendario editoriale.

## Come si usa

1. Aggiungi il plugin da **Personalizza → Plugin** in Claude.
2. Nella scheda **Connettori** del plugin collega AraWeb CRM: entra con la tua email e password del gestionale e premi **Consenti**.
3. Il titolare dell'attività deve aver acceso l'assistente AI una volta, da **Impostazioni → Assistente AI** nel gestionale.
4. Chiedi per esempio: «com'è la giornata?», «prepara un WhatsApp per i clienti che non vengono da tre mesi», «organizziamo il Cenone di Capodanno, 80 posti a 90 euro».

Istruzioni complete: [crm.araweb.cloud/collega-ai.html](https://crm.araweb.cloud/collega-ai.html).

## Dati

Il plugin è fatto solo di istruzioni in testo: non esegue programmi e non salva nulla. I dati passano soltanto tra Claude e il tuo account AraWeb CRM, tramite il connettore `crm.araweb.cloud/mcp`, con accesso OAuth. Il gestionale non manda messaggi ai clienti: Claude prepara i testi e li invii tu. Allergie, dati sulla salute e consensi non sono mai letti né modificati tramite AI. Ogni operazione resta nel registro del gestionale con l'indicazione «via AI». [Privacy policy](https://crm.araweb.cloud/privacy.html).

## Assistenza

[simone@araweb.cloud](mailto:simone@araweb.cloud)
