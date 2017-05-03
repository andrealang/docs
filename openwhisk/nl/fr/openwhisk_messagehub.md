---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-04"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Utilisation du package Message Hub
{: #openwhisk_catalog_message_hub}

Ce package vous permet de communiquer avec des instances [Message Hub](https://developer.ibm.com/messaging/message-hub) pour publier des messages de consommation via l'API hautes performances Kafka native.
{: shortdesc}

## Création d'un déclencheur qui écoute une instance IBM MessageHub
{: #openwhisk_catalog_message_hub_trigger}

Pour créer un déclencheur qui réagit lorsque des messages sont publiés dans une instance Message Hub, vous devez utiliser le flux nommé `/messaging/messageHubFeed`. Cette action de flux prend en charge les paramètres suivants :

|Nom|Type|Description|
|---|---|---|
|kafka_brokers_sasl|Tableau JSON de chaînes|Ce paramètre est un tableau de chaînes `<hôte>:<port>` qui comprend les courtiers de votre instance Message Hub|
|utilisateur|Chaîne|Votre nom d'utilisateur Message Hub|
|password|Chaîne|Votre mot de passe Message Hub|
|topic|Chaîne|Rubrique que vous souhaitez faire écouter par le déclencheur|
|kafka_admin_url|Chaîne d'URL|URL de l'interface REST d'administration de Message Hub|
|isJSONData|Booléen (facultatif - par défaut=false)|Lorsque ce paramètre a pour valeur `true`, le fournisseur tente de faire une analyse syntaxique de la valeur de message en tant que JSON avant de la transmettre en tant que contenu du déclencheur.|
|isBinaryKey|Booléen (facultatif - par défaut=false)|Lorsque ce paramètre reçoit la valeur `true`, le fournisseur encode la valeur de la clé en Base64 avant de la transmettre en tant que contenu du déclencheur.|
|isBinaryValue|Booléen (facultatif - par défaut=false)|Lorsque ce paramètre reçoit la valeur `true`, le fournisseur encode la valeur du message en Base64 avant de la transmettre en tant que contenu du déclencheur.|

Cette liste de paramètres peut vous sembler impressionnante, mais vous pouvez les définir automatiquement à l'aide de la commande d'interface de ligne de commande package refresh :

1. Créez une instance du service Message Hub sous l'organisation et l'espace en cours que vous utilisez pour OpenWhisk.

2. Vérifiez que la rubrique que vous souhaitez écouter existe déjà dans Message Hub ou créez une rubrique, par exemple, `mytopic`.

3. Actualisez les packages dans votre espace de nom. L'actualisation crée automatiquement une liaison de package pour l'instance de service Message Hub que vous avez créée.

  ```
  wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Message_Hub_Credentials-1
  ```

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Message_Hub_Credentials-1 private
  ```

  Votre liaison de package contient désormais les données d'identification associées à votre instance Message Hub.

4. A présent, il ne vous reste plus qu'à créer un déclencheur à exécuter lorsque de nouveaux messages sont publiés sur votre rubrique Message Hub.

  ```
  wsk trigger create MyMessageHubTrigger -f /myBluemixOrg_myBluemixSpace/Bluemix_Message_Hub_Credentials-1/messageHubFeed -p topic mytopic
  ```
  {: pre}

## Configuration d'un package Message Hub hors de Bluemix

Si vous voulez configurer votre service Message Hub hors de Bluemix, vous devez créer manuellement une liaison de package pour le service Message Hub. Pour ce faire, vous avez besoin des données d'identification et des informations de connexion du service Message Hub.

1. Créez une liaison de package configurée pour votre service Message Hub.

  ```
  wsk package bind /whisk.system/messaging myMessageHub -p kafka_brokers_sasl "[\"kafka01-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka02-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka03-prod01.messagehub.services.us-south.bluemix.net:9093\"]" -p user <your Message Hub user> -p password <your Message Hub password> -p kafka_admin_url https://kafka-admin-prod01.messagehub.services.us-south.bluemix.net:443
  ```
  {: pre}

2. A présent, vous pouvez créer un déclencheur à l'aide de votre nouveau package qui sera exécuté lorsque de nouveaux messages seront publiés sur votre rubrique Message Hub.

  ```
  wsk trigger create MyMessageHubTrigger -f myMessageHub/messageHubFeed -p topic mytopic -p isJSONData true
  ```
  {: pre}


## Ecoute de messages
{: #openwhisk_catalog_message_hub_listen}

Une fois le déclencheur créé, le  système surveille la rubrique indiquée dans votre service de messagerie. Lorsque de nouveaux messages sont publiés, le déclencheur est exécuté.

Le contenu de ce déclencheur comporte une zone `messages`, qui est un tableau des messages publiés depuis la dernière exécution du déclencheur. Chaque objet de message figurant dans le tableau contient les zones suivantes :
- topic
- partition
- offset
- key
- value

En Kafka, ces zones sont évidentes. Toutefois, `key` peut utiliser un paramètre `isBinaryKey` facultatif qui permet à `key` de transmettre des données binaires. Par ailleurs, `value` mérite une attention spéciale. Les zones facultatives `isJSONData` et `isBinaryValue` peuvent être utilisées pour le traitement des messages JSON et binaires. Les zones `isJSONData` et `isBinaryValue` ne peuvent pas être utilisées simultanément.

Par exemple, si `isBinaryKey` a reçu la valeur `true` lors de la création du déclencheur, `key` sera encodé sous forme de chaîne en Base64 lorsqu'il est renvoyé à partir du contenu d'un déclencheur exécuté.

Par exemple, si un élément `key` de `Some key` est transmis avec `isBinaryKey` défini à `true`, le contenu du déclencheur sera similaire à ceci :

```json
    {
    "messages": [
    {
            "partition": 0,
            "key": "U29tZSBrZXk=",
            "offset": 421760,
            "topic": "mytopic",
            "value": "Some value"
        }
    ]
}
```

Si le paramètre `isJSONData` a reçu la valeur `false` (ou n'a pas été défini du tout) lors de la création du déclencheur, la zone `value` correspondra à la valeur brute du message publié. Cependant, si `isJSONData` a été défini sur `true` à la création du déclencheur, le système tente d'analyser cette valeur pour le mieux en tant qu'objet JSON. Si l'analyse aboutit, la zone `value` du contenu du déclencheur sera l'objet JSON qui en résulte.

Par exemple, si un message `{"title": "Une chaîne", "amount": 5, "isAwesome": true}` est publié avec `isJSONData` défini sur `true`, le contenu du déclencheur sera similaire à ce qui suit :

```json
    {
  "messages": [
    {
      "partition": 0,
        "key": null,
        "offset": 421760,
        "topic": "mytopic",
        "value": {
          "amount": 5,
            "isAwesome": true,
            "title": "Une chaîne"
        }
    }
  ]
}
```

Cependant, si le même contenu de message est publié avec `isJSONData` défini sur `false`, le contenu du déclencheur sera similaire à l'exemple suivant :

```json
    {
  "messages": [
    {
      "partition": 0,
      "key": null,
      "offset": 421761,
      "topic": "mytopic",
      "value": "{\"title\": \"Une chaîne\", \"amount\": 5, \"isAwesome\": true}" }
  ]
}
```

A l'instar d' `isJSONData`, si `isBinaryValue` a reçu la valeur `true` lors de la création du déclencheur, l'élément `value` résultant dans le contenu du déclencheur sera encodé sous forme de chaîne en Base64.

Par exemple, si un élément `value` de `Some data` est transmis avec `isBinaryValue` défini à `true`, le contenu du déclencheur pourrait être similaire à ceci :

```json
    {
  "messages": [
    {
      "partition": 0,
      "key": null,
      "offset": 421760,
      "topic": "mytopic",
      "value": "U29tZSBkYXRh"
    }
  ]
}
```

Si le même message est publié sans que `isBinaryData` soit défini à `true`, le contenu du déclencheur serait similaire à l'exemple ci-dessous :

```json
    {
  "messages": [
    {
      "partition": 0,
      "key": null,
      "offset": 421760,
      "topic": "mytopic",
      "value": "Some data"
    }
  ]
}
```

### Les messages sont traités par lots
Vous remarquerez que le contenu du déclencheur comporte un tableau de messages. Cela signifie que si vous produisez des messages très rapidement vers votre système de messagerie, le flux tente de générer un lot à partir des messages publiés afin de les traiter en une seule exécution du déclencheur. Cela permet de publier les messages dans le déclencher de manière plus rapide et plus efficace.

Lorsque vous codez des actions exécutées par votre déclencheur, gardez à l'esprit que le nombre de messages du contenu est techniquement illimité, mais qu'il est toujours supérieur à 0. Voici un exemple de message par lots (notez la modification apportée à la valeur *offset*) :
 
 ```json
    {
   "messages": [
    {
         "partition": 0,
         "key": null,
         "offset": 100,
         "topic": "mytopic",
         "value": {
             "amount": 5
         }
       },
       {
         "partition": 0,
         "key": null,
         "offset": 101,
         "topic": "mytopic",
         "value": {
             "amount": 1
         }
       },
       {
         "partition": 0,
         "key": null,
         "offset": 102,
         "topic": "mytopic",
         "value": {
             "amount": 999
         }
       }
   ]
 }
 ```

## Production de messages vers Message Hub
Si vous désirez utiliser une action OpenWhisk pour produire facilement un message vers Message Hub, vous pouvez utiliser l'action `/messaging/messageHubProduce`. Cette action reçoit les paramètres suivants :

|Nom|Type|Description|
|---|---|---|
|kafka_brokers_sasl|Tableau JSON de chaînes|Ce paramètre est un tableau de chaînes `<hôte>:<port>` qui comprend les courtiers de votre instance Message Hub|
|utilisateur|Chaîne|Votre nom d'utilisateur Message Hub|
|password|Chaîne|Votre mot de passe Message Hub|
|topic|Chaîne|Rubrique dont le déclencheur doit être à l'écoute|
|value|Chaîne|Valeur pour le message que vous désirez générer|
|key|Chaîne (facultatif)|Clé du message que vous désirez générer|

Tandis que les trois premiers paramètres peuvent être liés automatiquement à l'aide `wsk package refresh`, ci-après figure un exemple d'appel de l'action avec tous les paramètres requis :

```
wsk action invoke /messaging/messageHubProduce -p kafka_brokers_sasl "[\"kafka01-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka02-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka03-prod01.messagehub.services.us-south.bluemix.net:9093\"]" -p topic mytopic -p user <your Message Hub user> -p password <your Message Hub password> -p value "This is the content of my message"
```
{: pre}

## Exemples

### Intégration d'OpenWhisk avec IBM Message Hub, Node Red, IBM Watson IoT, IBM Object Storage et IBM Data Science Experience
 [Cliquez ici](https://medium.com/openwhisk/transit-flexible-pipeline-for-iot-data-with-bluemix-and-openwhisk-4824cf20f1e0) pour consulter un exemple d'intégration OpenWhisk avec IBM Message Hub, Node Red, IBM Watson IoT, IBM Object Storage et le service IBM Data Science Experience (Spark).

## Références
- [IBM Message Hub](https://developer.ibm.com/messaging/message-hub/)
- [Apache Kafka](https://kafka.apache.org/)
