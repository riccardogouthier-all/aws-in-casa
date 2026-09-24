# Consegna — AWS in casa

**Nome e cognome:**
**Binario seguito:** A (piano gratuito) / B (piano studente)

---

## 1.5 — Pubblicare a mano

> Hai pubblicato in quattro comandi. Cosa succede se domani li sbagli, o se li lancia
> un tuo collega in ordine diverso?

**Ordine sbagliato** → fallimento a cascata:

**s3 sync prima di mb** → bucket inesistente, errore
**sync prima di website** → file caricati ma niente hosting statico attivo
**build.sh dopo sync** → pubblichi versione vecchia/vuota

**Comandi sbagliati/dimenticati:**

**--delete omesso** → bucket accumula file obsoleti, versioni vecchie restano raggiungibili
**--index-document omesso** → sito non serve pagina radice
**credenziali/endpoint non esportate** → Could not connect to endpoint URL

**Collega assente oggi:**

Non conosce sequenza esatta, nomi bucket, flag necessari
Nessuna fonte di verità unica: procedura vive solo nella tua testa/history del terminale
**Rischio:** rifà bucket con nome diverso, dimentica website, o salta build.sh → pubblica sorgenti non compilati

---

## 2.4 — Il changeset

> Cosa e' cambiato quando hai rilanciato il deploy dopo aver modificato ErrorDocument?
> Perche' CloudFormation non ha ricreato il bucket?

**Cambiato:** solo ErrorDocument (index.html→errore.html) applicato al bucket esistente, non ricreato.

**Perché CFN non ricrea:** stack = stato salvato. 
Confronta il template nuovo con lo stato precedente registrato → calcola changeset (diff) → applica solo differenza. 
Bucket logico invariato tra deploy → CFN aggiorna proprietà, non tocca mai la risorsa. 
Meccanismo identico a terraform plan: guarda cosa cambierebbe, poi applica solo quello.

Se qualcuno modifica a mano da console: stato salvato ≠ realtà → drift.

---

## Fase 3 / 4 — Binario B

> Incolla qui lo stato delle tre fasi della pipeline (output di list-action-executions)
> e allega gli screenshot.

_(risposta)_

> Quando hai messo il TODO, dove si e' fermata la pipeline e cosa e' rimasto online?

_(risposta)_

---

## Fase 3bis — Binario A

1. Quali tre stage ha la pipeline e cosa passa dall'uno all'altro?

_(risposta)_

2. Cosa fa CodePipeline che il tuo script bash non fa? (almeno tre cose)

_(risposta)_

3. Dove si vedrebbe la differenza se due persone lanciassero il deploy nello stesso momento?

_(risposta)_

---

## Chiusura — Dove l'emulatore mente

> Delle quattro crepe viste a lezione, quale e' la piu' pericolosa se ti fidi
> dell'emulatore e vai in produzione? Motiva.

_(risposta)_
