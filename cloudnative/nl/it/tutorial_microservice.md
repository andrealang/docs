---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Esercitazione end-to-end dello starter di base del microservizio 
{: #tutorial}

La seguente esercitazione end-to-end spiega i passi per creare un progetto da uno starter di base del microservizio, inclusi gli strumenti che devi avere installato e, successivamente, i passi per eseguire il codice del progetto. 

## Installazione degli strumenti per sviluppatori
{: #dev_tools}

Assicurati di aver installato gli [strumenti per sviluppatori prerequisiti ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](get_code.html#prereq-dev-tools){: new_window}.


## Creazione di un progetto utilizzando la {{site.data.keyword.dev_console}}
{: #create-devex}

1. Crea un progetto nella {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}}.

	1. Dalla pagina **Introduzione** nella {{site.data.keyword.dev_console}}, fai clic su **Crea progetto**.

		In alternativa puoi fare clic su **Crea progetto** dalla pagina **Progetti**.

	2. Seleziona **Microservizio** e fai clic su **Avanti**.

	3. Seleziona **Di base** e fai clic su **Avanti**.

	4. Immetti il nome del tuo progetto. Per questa esercitazione, utilizza `MicroserviceProject`.   

	5. Immetti un nome host. Per questa esercitazione, utilizza `devhost` 
   
	6. Fai clic su **Crea**.

2. Facoltativo: aggiungi la funzionalità Data.

	1. Fai clic su **Visualizza** per **Data** nella pagina **Panoramica progetto**.

      In alternativa, puoi fare selezionare **Crea** o **Aggiungi esistente** nella pagina **Funzionalità > Data**.

   2. Immetti il nome del tuo servizio e fai clic su **Crea**.

3. Genera il tuo codice del progetto.

	1. Fai clic su **Richiama codice** nella pagina **Panoramica progetto** per selezionare il tuo linguaggio.
   
		In alternativa puoi fare clic sulla pagina **Codice**.
      
	2. Fai clic su **Genera codice**.
   
	3. Quando il codice del progetto ha terminato la generazione, fai clic su **Scarica codice** per scaricare il tuo archivio del progetto.

4. Facoltativo: [Aggiorna il tuo progetto](project_overview_page.html#update_language) per generare un nuovo linguaggio.


## Creazione di un progetto utilizzando la {{site.data.keyword.dev_cli_notm}}
{: #create-cli}

1. Assicurati di aver installato la [{{site.data.keyword.dev_cli_short}}](dev_cli.html).

2. Nella tua finestra del terminale, passa a una directory locale di tua scelta ed esegui il seguente comando.
  
	```
	bx dev create
	```
	{: codeblock}

3. Fornisci i seguenti valori quando richiesto:

	* Seleziona un modello: 4 (per i microservizi)
	* Seleziona uno starter: 1 (di base)
	* Seleziona una piattaforma: 3 (per Java)
	* Immetti un nome per il tuo progetto: `MicroserviceProjectCLI`

4. Se desideri aggiungere servizi al tuo progetto, immetti `y` quando ti viene domandato e rispondi alle rimanenti domande.

5. Quando `MicroserviceProjectCLI` è stato correttamente salvato, passa alla cartella `MicroserviceProjectCLI`.

6. A questo punto potresti aggiungere il tuo proprio codice, creare o eseguire il progetto.
 
 
## Esecuzione di un progetto utilizzando la {{site.data.keyword.dev_cli_notm}} 
{: #running-dev-plugin}

1. Per creare il progetto nella tua directory del progetto corrente immetti il seguente comando:

	```
	bx dev build
	```     
	{: codeblock}

2. Per creare ed eseguire il progetto nella tua directory del progetto corrente immetti il seguente comando: 

	```
	bx dev run
	```
	{: codeblock}	

3. Puoi accedere all'applicazione utilizzando curl sul tuo server:

	```
	curl http://localhost:8080	
	```
	{: codeblock}
