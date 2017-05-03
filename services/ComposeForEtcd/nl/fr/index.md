---

copyright:
  years: 2016
lastupdated: "2016-12-09"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Initiation à {{site.data.keyword.composeForEtcd}}
{: #getting-started-with-compose-for-etcd}

etcd est un espace de stockage de paires clé-valeur contenant les données toujours correctes dont vous avez besoin afin de coordonner et gérer votre cluster de serveurs pour la gestion des configurations de serveur distribué. etcd utilise l'algorithme de consensus RAFT pour garantir la cohérence des données dans votre cluster. Il impose l'ordre dans lequel les opérations sont exécutées sur les données de manière à obtenir les mêmes résultats et de la même façon pour chaque noeud du cluster. {{site.data.keyword.composeForEtcd_full}} ajoute des sauvegardes automatiques des données de configuration stockées dans etcd. Une interface d'administration intuitive vous permet de surveiller, de mettre à l'échelle et d'administrer votre déploiement avec beaucoup plus de facilité.
{:shortdesc}

**Remarque :** Les instances de service Compose qui ont été mises à disposition avant le 14 septembre 2016 et qui sont toujours actives peuvent encore être utilisées et sont directement accessibles sur le site [https://www.compose.com/](https://www.compose.com). Les instances de service Compose mises à disposition depuis cette date sont directement accessibles et utilisables dans votre compte Bluemix.

Exécutez les étapes décrites ci-après pour commencer à utiliser {{site.data.keyword.composeForEtcd}}.

1. [Créez une instance {{site.data.keyword.composeForEtcd}}](https://console.ng.bluemix.net/catalog/services/compose-for-etcd/).

  Lorsque vous créez une instance du service, prenez soin de sélectionner un nom pour votre service et un nom de données d'identification. Laissez le service non lié ; vous pourrez connecter une application à votre service ultérieurement en utilisant les données d'identification fournies lors de la mise à disposition du service. La section *Données d'identification disponibles* répertorie les différentes valeurs de données d'identification.

2. Connectez-vous au service {{site.data.keyword.composeForEtcd}}.

Pour connecter une application à votre service, utilisez les données d'identification créées en même temps que le service. L'exemple d'application montre comment utiliser Node.js pour établir une connexion au service {{site.data.keyword.composeForEtcd}}.

Téléchargez l'exemple d'application [compose-etcd-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-etcd-helloworld-nodejs) et suivez les instructions contenues dans le fichier Readme. Ensuite, cliquez sur **Afficher l'application** sur la page des détails d'application pour afficher le contenu de la section *Exemples*.

## Données d'identification disponibles

Nom de zone|Description
----------|-----------
`ca_certificate_base64`|Certificat autosigné utilisé pour confirmer qu'une application se connecte bien au serveur approprié. Le certificat est codé en base64. Vous devez décoder la clé avant de l'utiliser, comme illustré dans l'exemple d'application.
`deployment_id`|Identificateur interne du service, créé dans Compose.
`db_type`|Type de base de données fourni par le service, en l'occurrence, `etcd`.
`name`|Nom du déploiement de base de données.
`uri`|URI à utiliser pour établir la connexion au service. `uri` comprend le schéma (`amqps:), le nom et le mot de passe administrateur, le nom d'hôte du serveur et le numéro de port auquel se connecter, ainsi que le nom `vhost.
{: caption="Table 1. {{site.data.keyword.composeForEtcd}} credentials" caption-side="top"}

# Liens connexes
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Compose Articles](https://www.compose.com/articles/){:new_window}

## Tutoriels et exemples
{: #samples}
* [compose-etcd-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-etcd-helloworld-nodejs){:new_window}

## Liens connexes
{: #general}
* [Aide sur Compose](https://help.compose.com/docs){:new_window}
