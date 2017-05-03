---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Utilizzo dell'SDK mobile {{site.data.keyword.openwhisk_short}}
{: #openwhisk_mobile_sdk}

{{site.data.keyword.openwhisk}} fornisce un SDK mobile per dispositivi iOS e watchOS che abilita le applicazioni mobili ad attivare facilmente dei trigger remoti e richiamare azioni remote. Una versione per Android non è attualmente disponibile; gli sviluppatori Android possono utilizzare la API REST {{site.data.keyword.openwhisk}} direttamente.

L'SDK mobile è scritto in  Swift 3.0 e supporta iOS 10 e release successive. Puoi costruire l'SDK mobile utilizzando Xcode 8.0. Le versioni Swift 2.2/Xcode 7 legacy dell'SDK sono disponibili fino alla 0.1.7, sebbene questa sia ora obsoleta.

## Aggiunta di SDK alla tua applicazione
{: #openwhisk_add_sdk}

Puoi installare l'SDK mobile utilizzando CocoaPods, Carthage oppure dalla directory di origine.

### Installazione utilizzando CocoaPods
{: #openwhisk_add_sdk_cocoapods}

L'SDK {{site.data.keyword.openwhisk_short}} per dispositivi mobili è disponibile per la distribuzione pubblica tramite CocoaPods. Ponendo che CocoaPods sia installato, inserisci le seguenti righe in un file denominato 'Podfile' all'interno della directory del progetto applicazione starter.

```
install! 'cocoapods', :deterministic_uuids => false
use_frameworks!

target 'MyApp' do
     pod 'OpenWhisk', :git => 'https://github.com/openwhisk/openwhisk-client-swift.git', :tag => '0.2.2'
end

target 'MyApp WatchKit Extension' do
     pod 'OpenWhisk', :git => 'https://github.com/openwhisk/openwhisk-client-swift.git', :tag => '0.2.2'
end
```
{: codeblock}

Nella riga di comando, digita `pod install`. Questo comando installa l'SDK per un'applicazione iOS con un'estensione watchOS.  Utilizza il file spazio di lavoro creato da CocoaPods per la tua applicazione, per l'apertura del progetto in Xcode.

Al termine dell'installazione, apri lo spazio di lavoro del tuo progetto.  Durante la creazione, potresti visualizzare la seguente avvertenza:
`Use Legacy Swift Language Version” (SWIFT_VERSION) is required to be configured correctly for targets which use Swift. Use the [Edit > Convert > To Current Swift Syntax…] menu to choose a Swift version or use the Build Settings editor to configure the build setting directly.`
Questo si verifica se Cocoapods non aggiorna la versione Swift nel progetto Pods.  Per correggere il problema, seleziona il progetto Pods e la destinazione {{site.data.keyword.openwhisk_short}}.  Vai a Build Settings e modifica l'impostazione `Use Legacy Swift Language Version` su `no`. In alternativa, puoi aggiungere le seguenti istruzioni di post installazione alla fine del tuo Podfile:

```
post_install do |installer|
  installer.pods_project.targets.each do |target|
    target.build_configurations.each do |config|
      config.build_settings['SWIFT_VERSION'] = '3.0'
    end
  end
end
```
{: codeblock}

### Installazione mediante Carthage
{: #openwhisk_add_sdk_carthage}

Crea un file nella directory del progetto della tua applicazione e denominalo 'Cartfile'. Inserisci la seguente riga nel file.
```
github "openwhisk/openwhisk-client-swift.git" ~> 0.2.2 # Or latest version
```
{: codeblock}

Nella riga di comando, digita `carthage update --platform ios`. Carthage scarica e genera l'SDK, crea una directory denominata Carthage nella directory del progetto della tua applicazione e inserisce un file {{site.data.keyword.openwhisk_short}}.framework all'interno di Carthage/build/iOS.

Devi quindi aggiungere {{site.data.keyword.openwhisk_short}}.framework ai framework integrati nel tuo progetto Xcode

### Installazione dal codice sorgente
{: #openwhisk_add_sdk_source}

Il codice sorgente è disponibile all'indirizzo https://github.com/openwhisk/openwhisk-client-swift.git.
Apri il progetto con `OpenWhisk.xcodeproj` utilizzando Xcode.
Il progetto contiene due schemi: "OpenWhisk" (destinato a iOS) e "OpenWhiskWatch" (destinato a watchOS 2).
Crea il progetto per le destinazioni richieste e aggiungi i framework risultanti alla tua applicazione (solitamente in ~/Library/Developer/Xcode/DerivedData/nome tua applicazione).

## Installazione dell'esempio di applicazione starter
{: #openwhisk_install_sdkstart}

Puoi utilizzare la CLI {{site.data.keyword.openwhisk_short}} per scaricare il codice di esempio che incorpora il framework SDK {{site.data.keyword.openwhisk_short}}.  

Per installare l'esempio di applicazione starter, immetti il seguente comando:
```bash
wsk sdk install iOS
```
{: pre}

Questo comando scarica un file compresso che contiene l'applicazione starter. Nella directory del progetto è presente un Podfile.

Per installare l'SDK, immetti il seguente comando:
```bash
pod install
```
{: pre}

## Introduzione all'SDK
{: #openwhisk_sdk_getstart}

Per essere rapidamente operativo, crea un oggetto WhiskCredentials con le tue credenziali API {{site.data.keyword.openwhisk_short}} e crea un'istanza {{site.data.keyword.openwhisk_short}} dall'oggetto.

Ad esempio, utilizza il seguente codice di esempio per creare un oggetto credenziali:

```swift
let credentialsConfiguration = WhiskCredentials(accessKey: "myKey", accessToken: "myToken")

let whisk = Whisk(credentials: credentialsConfiguration!)
```
{: codeblock}

Nell'esempio precedente, passi `myKey` e `myToken` che ottieni da {{site.data.keyword.openwhisk_short}}. Puoi richiamare la chiave e il token con il seguente comando CLI:

```bash
wsk property get --auth
```
{: pre}
```
whisk auth        kkkkkkkk-kkkk-kkkk-kkkk-kkkkkkkkkkkk:tttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttt
```
{: screen}

Le stringhe prima dei due punti rappresentano la tua chiave e la stringa dopo i due punti rappresenta il token.

## Richiamo di un'azione {{site.data.keyword.openwhisk_short}}
{: #openwhisk_sdk_invoke}


Per richiamare un'azione remota, puoi richiamare `invokeAction` con il nome dell'azione. Puoi specificare lo spazio dei nomi a cui appartiene l'azione o lasciare il campo vuoto per accettare lo spazio dei nomi predefinito. Utilizza un dizionario per passare i parametri all'azione come richiesto.

Ad esempio:

```swift
// In this example, we are invoking an action to print a message to the {{site.data.keyword.openwhisk_short}} Console
var params = Dictionary<String, String>()
params["payload"] = "Hi from mobile"

do {
    try whisk.invokeAction(name: "helloConsole", package: "mypackage", namespace: "mynamespace", parameters: params, hasResult: false, callback: {(reply, error) -> Void in
        if let error = error {
            //do something
            print("Errore di richiamo dell'azione \(error.localizedDescription)")
        } else {
            print("Action invoked!")
        }

    })
} catch {
    print("Errore \(error)")
}
```
{: codeblock}

Nell'esempio precedente, richiami l'azione `helloConsole` utilizzando lo spazio dei nomi predefinito.

## Attivazione di un trigger {{site.data.keyword.openwhisk_short}}
{: #openwhisk_sdk_fire}

Per attivare un trigger remoto, puoi richiamare il metodo `fireTrigger`. Passa i parametri come richiesto utilizzando un dizionario.

```swift
// In this example we are firing a trigger when our location has changed by a certain amount

var locationParams = Dictionary<String, String>()
locationParams["payload"] = "{\"lat\":41.27093, \"lon\":-73.77763}"

do {
    try whisk.fireTrigger(name: "locationChanged", package: "mypackage", namespace: "mynamespace", parameters: locationParams, callback: {(reply, error) -> Void in

        if let error = error {
            print("Errore di attivazione del trigger \(error.localizedDescription)")
        } else {
            print("Trigger attivato!")
        }
    })
} catch {
    print("Errore \(error)")
}
```
{: codeblock}

Nell'esempio precedente, attivi un trigger denominato `locationChanged`.

## Utilizzo di azioni che restituiscono un risultato
{: #openwhisk_sdk_actionresult}

Se l'azione restituisce un risultato, imposta hasResult su true nella chiamata invokeAction. Il risultato dell'azione viene restituito nel dizionario della risposta, ad esempio:

```swift
do {
    try whisk.invokeAction(name: "actionWithResult", package: "mypackage", namespace: "mynamespace", parameters: params, hasResult: true, callback: {(reply, error) -> Void in

        if let error = error {
            //do something
            print("Errore di richiamo dell'azione \(error.localizedDescription)")

        } else {
            var result = reply["result"]
            print("Got result \(result)")
        }


    })
} catch {
    print("Errore \(error)")
}
```
{: codeblock}

Per impostazione predefinita, l'SDK restituisce solo l'ID attivazione e qualsiasi risultato prodotto dall'azione richiamata. Per ottenere i metadati dell'intero oggetto risposta, che include il codice di stato della risposta HTTP, utilizza la seguente impostazione:

```swift
whisk.verboseReplies = true
```
{: codeblock}

## Configurazione dell'SDK
{: #openwhisk_sdk_configure}

Puoi configurare l'SDK per lavorare con diverse installazioni di {{site.data.keyword.openwhisk_short}} utilizzando il parametro baseURL. Ad esempio:

```swift
whisk.baseURL = "http://localhost:8080"
```
{: codeblock}

In questo esempio, utilizzi un'installazione in esecuzione sull'hostlocale:8080. Se non specifichi baseUrl, l'SDK mobile utilizza l'istanza in esecuzione in https://openwhisk.ng.bluemix.net.

Puoi passare una NSURLSession personalizzata nel caso tu richieda una gestione della rete speciale. Ad esempio, potresti avere una tua installazione di {{site.data.keyword.openwhisk_short}} che utilizza i certificati autofirmati.

```swift
// create a network delegate that trusts everything
class NetworkUtilsDelegate: NSObject, NSURLSessionDelegate {
    func URLSession(session: NSURLSession, didReceiveChallenge challenge: NSURLAuthenticationChallenge, completionHandler: (NSURLSessionAuthChallengeDisposition, NSURLCredential?) -> Void) {
        completionHandler(NSURLSessionAuthChallengeDisposition.UseCredential, NSURLCredential(forTrust: challenge.protectionSpace.serverTrust!))
    }
}

// crea una NSURLSession che utilizza il delegato di attendibilità
let session = NSURLSession(configuration: NSURLSessionConfiguration.defaultSessionConfiguration(), delegate: NetworkUtilsDelegate(), delegateQueue:NSOperationQueue.mainQueue())

// imposta l'SDK per utilizzare questa urlSession invece di quella condivisa predefinita
whisk.urlSession = session
```
{: codeblock}

### Supporto per i nomi completi
{: #openwhisk_sdk_configure_qual}

Tutte le azioni e tutti i trigger hanno un nome completo formato da uno spazio dei nomi, un pacchetto e un nome di azione o trigger. L'SDK può accettare questi elementi come parametri quando richiami un'azione o attivi un trigger. L'SDK fornisce anche una funzione che accetta un nome completo che si presenta come `/mynamespace/mypackage/nameOfActionOrTrigger`. La stringa del nome completo supporta dei valori predefiniti senza nome per gli spazio dei nomi e i pacchetti di cui tutti gli utenti {{site.data.keyword.openwhisk_short}} dispongono, quindi si applicano le seguenti regole di analisi:

- qName = "foo" dà come risultato spazio dei nomi = default, pacchetto = default, azione/trigger = "foo"
- qName = "mypackage/foo" dà come risultato spazio dei nomi = default, pacchetto = mypackage, azione/trigger = "foo"
- qName = "/mynamespace/foo" dà come risultato spazio dei nomi = mynamespace, pacchetto = default, azione/trigger = "foo"
- qName = "/mynamespace/mypackage/foo dà come risultato spazio dei nomi = mynamespace, pacchetto = mypackage, azione/trigger = "foo"

Tutte le altre combinazioni generano un errore WhiskError.QualifiedName. Pertanto, se utilizzi dei nomi completi, devi racchiudere la chiamata in un costrutto "`do/try/catch`".

### Pulsante SDK
{: #openwhisk_sdk_configure_button}

Per praticità, l'SDK include un `WhiskButton`, che estende il `UIButton` per consentirgli di richiamare le azioni.  Per utilizzare il `WhiskButton`, attieniti a questo esempio:

```swift
var whiskButton = WhiskButton(frame: CGRectMake(0,0,20,20))

whiskButton.setupWhiskAction("helloConsole", package: "mypackage", namespace: "_", credentials: credentialsConfiguration!, hasResult: false, parameters: nil, urlSession: nil)

let myParams = ["name":"value"]

// Richiamalo quando rilevi un evento di stampa, ad esempio in un'IBAction, per richiamare l'azione
whiskButton.invokeAction(parameters: myParams, callback: { reply, error in
    if let error = error {
        print("Spiacenti; si è verificato un errore: \(error)")
    } else {
        print("Operazione riuscita: \(reply)")
    }
})

// oppure, in alternativa, puoi configurare un pulsante "autonomo" che è in ascolto per eventi di selezione pulsante a esso relativi e richiama un'azione

var whiskButtonSelfContained = WhiskButton(frame: CGRectMake(0,0,20,20))
whiskButtonSelfContained.listenForPressEvents = true
do {

   // utilizza l'API di nome completo che richiede do/try/catch
   try whiskButtonSelfContained.setupWhiskAction("mypackage/helloConsole", credentials: credentialsConfiguration!, hasResult: false, parameters: nil, urlSession: nil)
   whiskButtonSelfContained.actionButtonCallback = { reply, error in

       if let error = error {
           print("Spiacenti, si è verificato un errore: \(error)")
       } else {
           print("Operazione riuscita: \(reply)")
       }
   }
} catch {
   print("Errore di configurazione del pulsante \(error)")
}
```
{: codeblock}
