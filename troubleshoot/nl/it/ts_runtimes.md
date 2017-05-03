---

copyright:
  years: 2015, 2017
  
lastupdated: "2017-01-10"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 


# Risoluzione dei problemi relativi ai runtime
{: #runtimes}

Potresti riscontrare dei problemi quando utilizzi i runtime {{site.data.keyword.Bluemix}}. In molti casi, puoi risolvere questi problemi seguendo pochi semplici passi.
{:shortdesc}


## Pacchetto di build obsoleto utilizzato quando viene eseguito il push di un'applicazione
{: #ts_loading_bp}

Potresti non essere in grado di utilizzare i componenti di pacchetti di build più recenti quando esegui il push di un'applicazione. Puoi utilizzare i pacchetti di build che hanno dei meccanismi integrati per impedire il caricamento di componenti obsoleti oppure puoi eliminare il contenuto nella directory cache della tua applicazione prima di eseguire il push o di preparare di nuovo l'applicazione. 

Quando esegui il push o prepari di nuovo un'applicazione dopo l'aggiornamento del pacchetto di build, i componenti del pacchetto di build più recenti non vengono caricati automaticamente. Di conseguenza, la tua applicazione utilizza i componenti del pacchetto di build obsoleti dalla cache. Gli aggiornamenti che sono stati applicati al pacchetto di build dall'ultima volta che hai eseguito il push dell'applicazione non vengono implementati.
{: tsSymptoms}

Alcuni pacchetti di build non sono configurati per scaricare automaticamente tutti i componenti aggiornati da Internet per garantirti di utilizzare sempre la versione più recente.
{: tsCauses} 

Puoi utilizzare dei pacchetti di build che hanno dei meccanismi integrati per evitare il caricamento di componenti obsoleti, come ad esempio i seguenti:
{: tsResolve}

  * [Pacchetto di build Java Cloud Foundry  ![icona link esterno](../icons/launch-glyph.svg "External link icon")](https://github.com/cloudfoundry/java-buildpack){: new_window}. Questo pacchetto di build ha un meccanismo integrato per garantire che venga utilizzata la versione più recente del pacchetto di build. Per ulteriori informazioni sulla modalità di funzionamento di questo meccanismo, consulta [extending-caches.md ![icona link esterno](../icons/launch-glyph.svg "External link icon")](https://github.com/cloudfoundry/java-buildpack/blob/master/docs/extending-caches.md){: new_window}. 
  * [Pacchetto di build Cloud Foundry Node.js  ![icona link esterno](../icons/launch-glyph.svg "External link icon")](https://github.com/cloudfoundry/nodejs-buildpack){: new_window}. Questo pacchetto di build fornisce una funzionalità simile utilizzando le variabili di ambiente. Per abilitare il pacchetto di build Node.js a scaricare i modulo nodo da Internet ogni volta, immetti il
seguente comando nell'interfaccia riga di comando cf: 	
  ```
  set NODE_MODULES_CACHE=false
  ```

Se il pacchetto di build che stai utilizzando non fornisce un meccanismo per caricare i componenti più recenti in modo automatico, puoi eliminare manualmente il contento nella directory cache ed eseguire nuovamente il push della tua applicazione. Utilizza la seguente procedura:

 1. Estrai mediante checkout un ramo di un pacchetto di build null, ad esempio https://github.com/ryandotsmith/null-buildpack. Per informazioni su come estrarre mediante check-out un ramo, consulta [Git Basics - Getting a Git Repository ![icona link esterno](../icons/launch-glyph.svg "External link icon")](http://www.git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository){: new_window}.  
 2. Aggiungi la seguente riga al file `null-buildpack/bin/compile` ed esegui il commit delle modifiche. Per informazioni su come eseguire il commit delle modifiche, consulta [Git Basics - Recording Changes to the Repository ![icona link esterno](../icons/launch-glyph.svg "External link icon")](http://www.git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository){: new_window}.
  ```
  rm -rfv $2/*
  ```
 3. Esegui il push della tua applicazione con il pacchetto di build null che è stato modificato per eliminare
la cache utilizzando il seguente comando. Dopo che hai completato questo passo, tutto il contenuto nella directory
cache della tua applicazione viene eliminato.
  ```
  cf push appname -p app_path -b <pacchetto_build_null_modificato>
  ```
 4. Esegui il push della tua applicazione con il pacchetto di build più recente che vuoi utilizzare servendoti del seguente comando: 
  ```
  cf push appname -p app_path -b <ultimo_pacchetto_build>
  ```
 
## Messaggi NOTICE dal pacchetto di build PHP
{: #ts_phplog}

Potresti visualizzare dei messaggi di log che contengono NOTICE. Puoi interrompere la registrazione di questi messaggi modificando il
livello di registrazione.	

Quando esegui il push di un'applicazione a {{site.data.keyword.Bluemix_notm}} utilizzando un pacchetto di build PHP, potresti visualizzare dei messaggi che contengono `NOTICE`:
{: tsSymptoms}

```
• 2015-01-26T15:00:59.70+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: [pool www] 'user' directive is ignored when FPM is not running as root
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: [pool www] 'user' directive is ignored when FPM is not running as root
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: fpm is running, pid 93
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: ready to handle connections
```
Nel pacchetto di build PHP, il parametro error_log definisce il livello di registrazione. Per impostazione predefinita, il valore del parametro `error_log`
è **stderr notice**. Il seguente esempio mostra la configurazione predefinita del livello di registrazione nel file `nginx-defaults.conf` del pacchetto di build PHP fornito da Cloud Foundry. Per ulteriori informazioni, vedi [cloudfoundry/php-buildpack ![icona link esterno](../icons/launch-glyph.svg "External link icon")](https://github.com/cloudfoundry/php-buildpack/blob/ff71ea41d00c1226d339e83cf2c7d6dda6c590ef/defaults/config/nginx/1.5.x/nginx-defaults.conf){: new_window}.
{: tsCauses} 

```
daemon off;
error_log stderr notice;
pid @{HOME}/nginx/logs/nginx.pid;
```
	
I messaggi `NOTICE` sono solo informativi e potrebbero non indicare un problema. Puoi interrompere la registrazione di questi messaggi modificando il livello di registrazione da `stderr notice` a `stderr error` nel file nginx-defaults.conf del tuo pacchetto di build. Ad
esempio: 	
{: tsResolve}

```
daemon off;
error_log stderr error;
pid @{HOME}/nginx/logs/nginx.pid;
```
Per ulteriori informazioni su come modificare la configurazione di registrazione predefinita, vedi [error_log ![icona link esterno](../icons/launch-glyph.svg "External link icon")](http://nginx.org/en/docs/ngx_core_module.html#error_log){: new_window}.
	

## Impossibile importare una libreria Python di terze parti in {{site.data.keyword.Bluemix_notm}}
{: #ts_importpylib}

Potresti non riuscire a importare una libreria Python di terze parti
in {{site.data.keyword.Bluemix_notm}}. Per risolvere il problema, aggiungi i file di configurazione alla directory root della tua applicazione Python.

Quando tenti di importare una libreria Python di terze parti, come
la libreria `web.py`, il comando `cf push`
non riesce.
{: tsSymptoms}

Informazioni di configurazione mancanti per l'applicazione Python.
{: tsCauses}

Aggiungi un file `requirements.txt` e un file `Procfile` alla directory root della tua applicazione Python. Le seguenti informazioni presumono che tu stia importando la libreria `web.py`:
{: tsResolve}

 1. Aggiungi un file `requirements.txt` alla directory root della tua applicazione Python.
 
 Il file `requirements.txt` specifica i pacchetti di libreria richiesti per l'applicazione Python e la versione dei pacchetti.  Il seguente esempio mostra il contenuto del file `requirements.txt`, dove `web.py==0.37` indica
che la versione della libreria `web.py` che verrà scaricata è la 0.37 e `wsgiref==0.1.2` indica che la versione dell'interfaccia gateway del server Web richiesta dalla libreria web.py è la 0.1.2.
	 ```
	 web.py==0.37
     wsgiref==0.1.2
	 ```
	 Per ulteriori informazioni su come configurare
il file `requirements.txt`, vedi [Requirements files](https://pip.readthedocs.org/en/1.1/requirements.html). 
	 
 2. Aggiungi un file `Procfile` alla directory root della tua applicazione Python.
 Il file `Procfile` deve contenere il comando di avvio per la tua applicazione Python. Nel seguente comando, *ilnomedellatuaapplicazione* è il nome della tua applicazione Python e *PORT* è il numero di porta che l'applicazione Python dovrà utilizzare per ricevere le richieste dagli utenti dell'applicazione. *$PORT* è facoltativo. Se non specifichi una PORTA nel comando di avvio, verrà utilizzato il numero di porta indicato nella variabile di ambiente `VCAP_APP_PORT` che si trova all'interno dell'applicazione.  
	```
	web: python <ilnomedellatuaapplicazione>.py $PORT
	```

Puoi ora importare la libreria Python di terze parti in {{site.data.keyword.Bluemix_notm}}.	


## Il pulsante Azioni nella pagina Dettagli istanza è disabilitato
{: #ts_actionsbutton}

Il pulsante Azioni nella pagina Dettagli istanza è disabilitato.
{: tsSymptoms} 

Questo problema si verifica per i seguenti motivi:
{: tsCauses}

 * L'applicazione non è un'applicazione web Java&trade;. RMU (Runtime Management Utilities) supporta solo le applicazioni Web distribuite con i pacchetti di build Liberty.
 * L'applicazione non è distribuita con il pacchetto di build Liberty integrato.
 * L'applicazione è stata distribuita con una versione precedente del pacchetto di build Liberty.

Se il problema è causato da una versione precedente del pacchetto di build Liberty, ridistribuisci l'applicazione in {{site.data.keyword.Bluemix_notm}}. In caso contrario, puoi
fornire i seguenti file di log dell'applicazione client al team
di supporto:
{: tsResolve} 

  * logs/messages.log
  * logs/stdout.log
  * logs/stderr.log
 
  
## Sono richieste le credenziali per aprire la finestra di traccia o di dump
{: #ts_username}

Vengono richiesti un nome utente e una password per aprire la finestra di traccia o di dump.
{: tsSymptoms}

Questo problema si verifica a causa del timeout della sessione di accesso.
{: tsCauses}

Immetti di nuovo il nome utente e la password.
{: tsResolve}


## Si verifica un errore durante l'esecuzione delle operazioni di traccia o di dump
{: #ts_target}

Viene visualizzato un messaggio di errore mentre le operazioni di
traccia o di dump sono in esecuzione. Il messaggio indica che un'istanza di destinazione per un'applicazione non si trova nello stato di In esecuzione:
{: tsSymptoms}

```
Istanza 0: La specifica di traccia è stata impostata correttamente
Istanza 2: La specifica di traccia è stata impostata correttamente
Istanza 1: L'istanza di destinazione 1 per l'applicazione abcd non si trova nello stato di In esecuzione.
Istanza 3: La specifica di traccia è stata impostata correttamente
Istanza 4: La specifica di traccia è stata impostata correttamente
```

Questo problema si verifica per i seguenti motivi:
{: tsCauses} 

  * Le capacità di gestione della traccia o del dump riguardano solo le istanze dell'applicazione che sono in esecuzione. Le operazioni di traccia o di dump non possono essere utilizzate su istanze dell'applicazione arrestate, in fase di avvio o bloccate.
  * Lo stato dell'istanza dell'applicazione cambia quando si apre la finestra di dialogo della traccia o del dump. 

Chiudi la finestra e poi riaprila.
{: tsResolve} 


## Le istanze hanno configurazioni traceSpecification diverse
{: #ts_different_config}

Per diverse istanze di un'applicazione, potresti vedere configurazioni traceSpecification differenti.
{: tsSymptoms}

Questo comportamento si verifica per i seguenti motivi:
{: tsCauses}

  * Hai precedentemente modificato la configurazione per una o più istanze. Se modifichi la configurazione traceSpecification per una istanza, la modifica non viene applicata alle altre istanze della stessa applicazione. Ad esempio, la tua applicazione utilizza log4j e tu hai 2 istanze per questa applicazione. Puoi modificare il livello di log dell'istanza 0 da info a debug ma il livello di log dell'istanza 1 rimane info.
  
  * Viene eseguito un ridimensionamento incrementale dell'applicazione, che presenta delle nuove istanze. RMU non applica la configurazione traceSpecification dell'istanza esistente alla nuova istanza ridimensionata. La nuova istanza utilizza la configurazione predefinita. Ad esempio, la tua applicazione utilizza log4j e ha una istanza. Puoi modificare il livello di log di questa istanza da info a debug. Dopo che hai apportato questa modifica, se esegui il ridimensionamento incrementale della tua applicazione a due istanze, il livello di log della nuova istanza è info, invece di debug.

Nessuna azione richiesta. Questo è il comportamento previsto.
{: tsResolve} 


## Quota disco superata
{: #ts_diskquota}

Nel log dell'applicazione, potresti notare che la quota del disco è stata superata.

Nel log della tua applicazione vedi il messaggio di errore `Disk quota exceeded`.
{: tsSymptoms}

Questo problema si verifica per uno dei seguenti motivi:
{: tsCauses} 

  * I file di dump vengono generati con le istanze dell'applicazione in esecuzione e i file utilizzano la quota di disco assegnata. Per impostazione predefinita, la quota del disco per un'istanza dell'applicazione è di 1 GB. Puoi controllare l'utilizzo del
disco facendo clic su **Dashboard>Applicazione>Runtime applicazione**. Il seguente esempio mostra le informazioni di runtime, incluso l'utilizzo del disco, per due istanze di un'applicazione:
    ```
    Instance	State	CPU	Memory Usage	Disk Usage

	0		Running	1.0%	344.8MB/512MB	236.8MB/1GB
	2		Running	2.3%	361.2MB/512MB	235.7MB/1GB
    ```
  * La quota del disco è limitata dalla quota dell'organizzazione corrente.

Utilizza uno dei seguenti metodi:
{: tsResolve} 

  * Elimina i file di dump dopo averli scaricati.
  * Ridistribuisci l'applicazione con una quota di disco maggiore includendo la seguente voce nel manifest di distribuzione:
    ```
	disk_quota: 2048
	```
	
