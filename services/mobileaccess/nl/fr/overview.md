---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# À propos de {{site.data.keyword.amashort}}
{: #mca-overview}


Le service {{site.data.keyword.amafull}} fournit un service d'authentification aux applications mobiles et Web accédant au
ressources de cloud hébergées sur {{site.data.keyword.Bluemix_notm}}.

Vous pouvez utiliser le service {{site.data.keyword.amashort}} pour protéger les applications Node.js et Liberty for Java&trade; hébergées sur {{site.data.keyword.Bluemix_notm}} avec différents types d'authentification. L'instrumentation de vos applications mobiles avec le SDK de {{site.data.keyword.amashort}} vous permet d'utiliser les capacités d'authentification du service {{site.data.keyword.amashort}}. Utilisez le tableau de bord
{{site.data.keyword.amashort}} pour configurer les divers types d'authentification et examiner les données
collectées et envoyées par le SDK côté client.

**Remarque** : L'ancien nom du service {{site.data.keyword.amashort}} est Advanced Mobile Access.

## Composants
{: #components}

* **Tableau de bord {{site.data.keyword.amashort}}** : configurez différents types d'authentification

* **SDK client de {{site.data.keyword.amashort}}** : Instrumenter les applications mobiles pour leur permettre d'utiliser les fonctionnalités {{site.data.keyword.amashort}}. Plateformes
prises en charge : iOS 8+, Android 4+, Cordova et applications Web.

* **SDK serveur de {{site.data.keyword.amashort}}** : Protéger les ressources hébergées sur {{site.data.keyword.Bluemix_notm}}. Les contextes d'exécution pris en charge actuellement sont Node.js et Liberty for Java&trade;.

## Types d'authentification
{: #authtypes}
Vous pouvez utiliser les types d'authentification suivants dans votre appli mobile :

* **Facebook** : Utilisez Facebook en tant que fournisseur d'identité. Vos utilisateurs se connectent à l'appli mobile ou Web avec leurs données d'identification Facebook.

* **Google** : Utilisez Google en tant que fournisseur d'identité. Vos utilisateurs se connectent à l'appli mobile ou Web avec leurs données d'identification Google+.

* **Personnalisée**: Créez votre propre fournisseur d'identité. Vous contrôlez entièrement les types d'informations collectées et validées.

## Présentation de l'architecture
{: #architecture}

![Diagramme de présentation de l'architecture](images/mca-overview.jpg)

* Protégez vos ressources de cloud (applications Node.js) avec le SDK serveur de {{site.data.keyword.amashort}}.

* Utilisez la classe `Request` fournie par le SDK client de {{site.data.keyword.amashort}} pour communiquer avec vos ressources de cloud protégées.

* Le SDK serveur de {{site.data.keyword.amashort}} détecte une demande non autorisée et renvoie une demande d'autorisation HTTP 401.

* Le SDK client de {{site.data.keyword.amashort}} détecte la demande d'autorisation HTTP 401 et lance automatiquement le processus d'authentification
avec le service {{site.data.keyword.amashort}}.

* Une tentative d'authentification Facebook, Google ou personnalisée est lancée.

* Après une authentification réussie, {{site.data.keyword.amashort}} renvoie un jeton d'autorisation.

* Le SDK client de {{site.data.keyword.amashort}} ajoute automatiquement le jeton d'autorisation à la demande d'origine et renvoie la demande à la
ressource de cloud.

* Le SDK serveur de {{site.data.keyword.amashort}} extrait le jeton d'accès de la demande et le valide auprès du service
{{site.data.keyword.amashort}}.

* L'accès est accordé.  La réponse est renvoyée à l'application mobile.

## Flux de requête
{: #flow}
Le diagramme suivant illustre le flux d'une requête depuis le SDK client vers votre application back end
mobile et les fournisseurs d'identité.

![Diagramme de flux de demande](images/mca-sequence-overview.jpg)

* Utilisez le SDK {{site.data.keyword.amashort}} pour envoyer une demande à vos ressources de back end qui sont protégées par le SDK serveur de {{site.data.keyword.amashort}}.
* Le SDK serveur de {{site.data.keyword.amashort}} détecte une demande non autorisée et renvoie une erreur HTTP 401 et la portée d'autorisation.
* Le SDK client de {{site.data.keyword.amashort}} détecte automatiquement l'erreur HTTP 401 et lance le processus d'authentification.
* Le SDK client de {{site.data.keyword.amashort}} contacte le service {{site.data.keyword.amashort}} et lui demande d'émettre un en-tête d'autorisation.
* Le service {{site.data.keyword.amashort}} demande à l'app client de s'authentifier en fournissant une demande d'authentification conforme au type d'authentification configuré.
* D'après le type d'authentification, SDK client {{site.data.keyword.amashort}} :
   * Authentification Facebook ou Google : traite automatiquement la demande d'authentification
   * Authentification personnalisée : obtient les données d'identification selon la logique fournie par le développeur.
* Si l'authentification Facebook ou Google est configurée, le SDK client de {{site.data.keyword.amashort}} utilise le SDK associé pour obtenir les jetons d'accès Facebook ou Google. Ces jetons servent de réponse à la demande d'authentification.
* Si l'authentification personnalisée est configurée, le développeur doit obtenir la réponse à la demande d'authentification et la fournir au SDK client de
{{site.data.keyword.amashort}}.
* La réponse à la demande d'authentification obtenue est envoyée au service {{site.data.keyword.amashort}}.
* Le service valide la réponse à la demande d'authentification auprès du fournisseur d'identité concerné (Facebook/Google/authentification personnalisée).
* Si la validation aboutit, le service {{site.data.keyword.amashort}} génère un en-tête d'autorisation et le renvoie au SDK client de
{{site.data.keyword.amashort}}. L'en-tête d'autorisation contient deux jetons : un jeton qui contient des informations sur les droits d'accès, et un autre jeton qui contient des informations sur l'utilisateur, l'appareil et l'application.
* A partir de ce moment, toutes les demandes faites avec le SDK client de {{site.data.keyword.amashort}} contiennent un nouvel en-tête d'autorisation.
* Le SDK client de {{site.data.keyword.amashort}} renvoie automatiquement la demande d'origine qui avait déclenché le flux d'autorisation.
* Le SDK serveur de {{site.data.keyword.amashort}} extrait l'en-tête d'autorisation de la demande, la valide auprès du service {{site.data.keyword.amashort}} et donne l'accès à la ressource de back end.


## Aide et support pour {{site.data.keyword.amashort}}
{: #gettinghelp}

Si vous avez des problèmes ou des questions quand vous utilisez {{site.data.keyword.amashort}}, vous pouvez obtenir de l'aide en recherchant des informations précises ou en posant des questions via un forum. Vous pouvez aussi ouvrir un ticket de demande de service. 

Quand vous utilisez les forums pour poser une question, prenez soin d'étiqueter cette dernière de façon à ce qu'elle soit vue par les équipes de développement {{site.data.keyword.Bluemix_notm}}.

* En cas de questions d'ordre technique sur le développement et le déploiement d'une application avec {{site.data.keyword.amashort}}, postez votre question sur le forum [Stack Overflow ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://stackoverflow.com/search?q={{site.data.keyword.amashort}}+ibm-bluemix "Icône de lien externe"){: new_window} en lui adjoignant les balises "ibm-bluemix" et "{{site.data.keyword.amashort}}".
* Pour les questions relatives au service et aux instructions de mise en route, lancez une recherche sur le forum [IBM developerWorks ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=mobile+client+access%20%2B[bluemix] "Icône de lien externe"){: new_window}.. 

Voir la rubrique expliquant comment [obtenir de l'aide](https://www.{DomainName}/docs/support/index.html#getting-help) pour plus de détails sur l'utilisation des forums.

Pour plus d'informations sur l'ouverture d'un ticket de demande de service IBM, sur les niveaux de support disponibles ou les niveaux de gravité des tickets, voir la rubrique décrivant [comment contacter le support](https://www.{DomainName}/docs/support/index.html#contacting-support).

