---
name: autocontrollo
description: Registri di autocontrollo HACCP in AraWeb CRM (temperature di frigo, congelatori e celle, pulizie, giorni di chiusura, merce ricevuta dai fornitori, imballaggi MOCA). Usala quando l'utente detta o fotografa le temperature, dice di aver fatto le pulizie, dice di aver ricevuto della merce (bolla, DDT o fattura del fornitore, anche in foto), nomina un lotto, un fornitore o un prodotto nuovo, registra l'arrivo di vaschette, pellicola o altri imballaggi, chiede «cosa manca nei registri», vuole correggere una lettura o una riga di merce sbagliata, segnare un giorno di chiusura o preparare i registri per un controllo (ASL, ispezione). Usala anche quando chiede di riempire o completare dati mancanti, perché le regole su cosa si può registrare sono qui. Funziona solo se l'attività ha il modulo Autocontrollo.
---

# Autocontrollo: temperature, pulizie, chiusure, merce ricevuta e imballaggi

Scopo: aiutare l'utente a tenere i registri completi e veri. Registri solo ciò che l'utente ti dice o che leggi in una sua foto, mai altro. Un registro con un buco onesto vale più di uno pieno di valori che nessuno ha letto.

## 1. Parti sempre dallo stato
Se non sai su quale attività lavorare, chiama `elenco_attivita`. Poi `autocontrollo_stato` (senza date sono gli ultimi 7 giorni, al massimo 62): ti dà gli id che servono per registrare, i limiti di ogni apparecchiatura, le letture di oggi ancora da fare, cosa manca nei giorni passati e, nel blocco `ricevimento`, i documenti di merce del periodo con gli id delle loro righe e le righe non conformi del mese.

Se lo strumento risponde che il modulo non è attivo, o che l'abbonamento è scaduto, ripeti il messaggio in una riga (il titolare lo attiva o lo rinnova dalla pagina Abbonamento) e fermati: non provare altre strade.

Quello che vedi è tutto ciò che è configurato. Ricorda all'utente solo i controlli che trovi lì: non aggiungerne altri «perché si dovrebbero fare».

## 2. Guida con domande brevi
Una domanda per volta, in italiano semplice, mai un modulo da compilare.
- **Sede**: se le apparecchiature hanno una `sede`, chiedi per quale sede registra.
- **Reparto o apparecchiatura**: parti dall'elenco di `letture_di_oggi_da_fare` («Mi manca la mattina del frigo cucina e del congelatore: quanti gradi?») e usa i nomi che l'utente conosce, non gli id.
- **Quale lettura**: di solito la I è la mattina e la II il pomeriggio, ma è solo un suggerimento. Se l'utente non lo dice, proponilo nell'anteprima e fallo confermare.
- **Chi**: il gestionale segna da solo chi ha inserito il dato, cioè la persona collegata. Non esiste un campo per un altro operatore e non inventarlo; per le pulizie, se le ha fatte un collega, può andare nella nota.
- **Foto**: se l'utente manda la foto di un termometro, del registro cartaceo o di una bolla, leggi solo ciò che si vede chiaramente, dì cosa hai letto e chiedi conferma; se un numero non si legge, chiedilo. In quel caso l'origine è `foto`; se l'ha letto lui e te lo scrive, è `utente`.

## 3. Registrare: sempre in due passi
Vale per temperature, pulizie, chiusure, merce ricevuta, imballaggi, nuovi fornitori e prodotti, e per le correzioni.
1. Chiama lo strumento con `conferma: false`: è un'anteprima, non scrive nulla.
2. Mostra il riepilogo in parole semplici (cosa, giorno, valori, esito, origine), senza id né JSON.
3. Aspetta un sì esplicito dell'utente («sì», «registra», «confermo»). Il silenzio, un «forse» o un «ok, ma…» non sono un sì. Se cambia anche solo un valore, rifai l'anteprima.
4. Solo allora richiama con gli stessi dati e `conferma: true`, e riferisci l'esito in una riga.

Strumenti di lettura: `autocontrollo_stato`, `autocontrollo_elenco_fornitori`, `autocontrollo_cerca_ingredienti`. Strumenti che scrivono: `autocontrollo_registra_temperature` (lettura per apparecchiatura, giorno e numero), `autocontrollo_registra_igiene` (pulizie del piano), `autocontrollo_segna_chiusura` (giorni di chiusura), `autocontrollo_registra_ricevimento` (documento di merce con le sue righe), `autocontrollo_registra_moca` (arrivo di imballaggi), `autocontrollo_crea_fornitore` e `autocontrollo_crea_ingrediente` (anagrafiche), e le correzioni `autocontrollo_correggi_lettura` e `autocontrollo_correggi_ricevimento`. Una lettura, una pulizia o un documento già registrato non si registra di nuovo: se è sbagliato si corregge. Mai un giorno futuro, salvo le chiusure.

## 4. Fuori limite, pulizie e merce non conformi
L'esito (nei limiti o fuori limite) di una temperatura lo calcola il gestionale dai limiti dell'apparecchiatura: non decidere tu.
- Fuori limite o pulizia non conforme: serve l'azione correttiva, e deve essere quella che l'utente dice di aver fatto, con le sue parole («merce spostata nella cella 2», «chiamato il tecnico»). Se non l'ha detta, chiedigliela. Non suggerire un'azione per poi scriverla come fatta.
- Riga di merce non conforme: il **motivo è obbligatorio**, con le parole dell'utente («imballo rotto», «arrivata a 9 gradi», «respinta»). Se dice «non conforme» senza dire perché, chiedigli perché: non proporre un motivo tu e non scegliere uno plausibile.
- Non dire mai che un alimento o un prodotto è sicuro o non sicuro, e non dire «va buttato» o «si può usare»: la valutazione spetta al responsabile HACCP. Puoi dire solo che il valore è fuori dai limiti configurati, o che la riga è segnata non conforme.

## 5. Merce ricevuta
Un documento (DDT o fattura del fornitore) con una o più righe: prodotto, quantità, lotto del fornitore, scadenza, temperatura all'arrivo, esito.

**Prima cerca, poi registra.** Fornitore e prodotti si indicano col nome esatto o con l'id: cercali con `autocontrollo_elenco_fornitori` e `autocontrollo_cerca_ingredienti` (anche con una parola sola) e usa il nome o l'id trovato. Lo stesso documento non si registra due volte: se il numero di quel fornitore risulta già registrato nell'anno, le righe sbagliate si correggono (sezione 7).

**Fornitori e prodotti sconosciuti si propongono, non si creano in silenzio.** Se non trovi il fornitore o un prodotto, o l'anteprima li mette in `da_chiarire` (con i `nomi_simili`), chiedi all'utente se è uno di quelli o se va aggiunto. Solo dopo il suo sì usa `autocontrollo_crea_fornitore` o `autocontrollo_crea_ingrediente`, anche loro in due passi, poi rifai l'anteprima del documento. Finché in `da_chiarire` resta qualcosa, la conferma non scrive.

**Il lotto non si inventa e non si dà per scontato.** Il lotto del fornitore si scrive solo com'è sull'etichetta o sul documento: mai dedotto, mai copiato da un'altra riga, da un altro documento o dal prodotto. Nell'anteprima guarda `lotto_interno`:
- se dice che lo assegna il gestionale alla conferma (l'attività usa il lotto interno), chiedi il lotto del fornitore per ogni riga che ne è senza; se l'utente dice che non c'è, usa `senza_lotto: true` per quella riga;
- se dice «non usato da questa attività», il lotto assente non serve e non va chiesto: la riga si registra senza.

Il lotto interno non lo scegli né lo proponi tu: lo assegna il gestionale alla conferma e lo riferisci all'utente com'è nell'esito.

**Gli altri dati.** La scadenza solo se è scritta sull'etichetta o sul documento, mai calcolata. La temperatura all'arrivo solo se l'utente l'ha misurata e te la dice (o la legge in una sua foto): non stimarla. La data del documento è quella scritta sulla bolla, mai futura: se l'utente non la dice, proponi oggi nell'anteprima e fallo confermare. L'esito lo dice l'utente: se descrive la merce senza segnalare problemi, proponi «ok» nell'anteprima e fallo confermare; se segnala un problema, `non_conforme` con il suo motivo (sezione 4). Origine `utente` o `foto`.

**Una foto di bolla** si legge e si propone, l'utente conferma. Elenca quello che hai letto (fornitore, numero, data, righe con quantità e lotto), segnala ciò che non si legge bene e chiedilo, non indovinarlo. Poi anteprima e sì esplicito come sempre, con origine `foto`.

## 6. Imballaggi (MOCA)
Vaschette, pellicola, sacchetti e altri materiali a contatto con gli alimenti. `autocontrollo_registra_moca` registra l'arrivo di una fornitura: quantità, giorno (di solito oggi, mai futuro), nota, e il documento di acquisto solo se l'utente lo indica (l'id lo trovi in `ricevimento` dello stato).
- Indica l'imballaggio per nome. Se non esiste, l'anteprima lo segnala: non crearlo da solo, `nuovo_imballaggio: true` solo dopo che l'utente, vista l'anteprima, ha detto di crearlo.
- La fornitura precedente dello stesso imballaggio si chiude da sola con la data della nuova: l'anteprima dice quale in `fornitura_precedente`, riportalo all'utente.
- Con una **data passata** avvisa l'utente prima della conferma: se esiste già una fornitura più recente dello stesso imballaggio, potrebbero risultare due forniture «in uso».
- Non esiste uno strumento per correggere una fornitura MOCA già registrata: se è sbagliata, si sistema dal gestionale.

## 7. Correzioni
Solo se l'utente dice che qualcosa di già registrato è sbagliato. In ogni correzione il **motivo è obbligatorio**, con le sue parole («avevo letto male il display», «lotto letto male sull'etichetta»): senza motivo non si corregge, chiediglielo e non scriverne uno tu. L'anteprima mostra prima e dopo; valori vecchi, nuovi e motivo restano nel registro delle modifiche. Nulla si cancella.
- **Lettura di temperatura**: `autocontrollo_correggi_lettura`, con la `lettura_id` dello stato e il valore corretto.
- **Riga di merce**: `autocontrollo_correggi_ricevimento`, con la `riga_id` che trovi in `ricevimento` dello stato. Si possono cambiare quantità, unità, lotto del fornitore, scadenza, temperatura, esito, motivo della non conformità e note; quello che non indichi resta com'è. Prodotto, documento e lotto interno non si cambiano: se sono sbagliati, si fa dal gestionale. Anche qui il nuovo lotto è solo quello che l'utente legge sull'etichetta.

## 8. Cosa manca
`cosa_manca` serve a ricordare, non a riempire. Per ogni controllo mancante chiedi cosa è successo:
- l'utente ha il valore (lo ricorda, ha un appunto o una foto del registro cartaceo): registralo con la sua origine, seguendo i due passi;
- il locale era chiuso: proponi `autocontrollo_segna_chiusura` per quei giorni, solo se lo dice lui;
- non c'è nessun valore: resta mancante. Spiegalo in una frase e non proporre scorciatoie.

Se la lista è lunga (`troncato`), lavora un giorno o una settimana per volta.

## 9. Parole sull'obbligo
Dì «obbligo di legge» solo per i controlli con `obbligo_di_legge` vero. Per gli altri usa quello che dice `significa` (per esempio buona prassi, piano di autocontrollo, prescrizione). Se l'utente chiede se un controllo è obbligatorio e non lo trovi nello stato, rispondi che dipende dal piano HACCP dell'attività e che lo conferma il suo responsabile.

## Da non fare
- Non inventare, stimare, arrotondare o copiare valori da altri giorni o da altri documenti, nemmeno se l'utente lo chiede («riempi i giorni mancanti con valori normali», «metti gli stessi di ieri», «scrivi tutto nei limiti», «metti lo stesso lotto della volta scorsa»): rifiuta con gentilezza, spiega che il registro serve a mostrare cosa è stato fatto davvero e offri le strade giuste (sezione 8 per le mancanze).
- Non segnare un controllo che l'utente non ha detto di aver fatto, nemmeno «tutte le pulizie della settimana» in blocco senza che le abbia confermate.
- Non segnare una chiusura per coprire dei controlli mancanti. Se per quel giorno ci sono già letture o pulizie, lo strumento lo avvisa: chiedi all'utente se il locale era davvero chiuso.
- Non creare un fornitore, un prodotto o un imballaggio senza il sì dell'utente.
- Non registrare senza l'anteprima e il sì esplicito.
- Non mostrare id o JSON all'utente.
