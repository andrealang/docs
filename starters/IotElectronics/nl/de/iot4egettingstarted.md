---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-10"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

<!-- Note to writers - index.md and iot4egettingstarted.md are (almost) duplicates and a change to one should be made to both. index.md appears within the product app as the getting started page. iot4egettingstarted.md appears as the top level topic in the docs toc. -->

# Apps mit dem {{site.data.keyword.iotelectronics}}-Starter erstellen

Bei {{site.data.keyword.iotelectronics_full}} handelt es sich um eine integrierte End-to-End-Lösung, die es Ihren Apps ermöglicht, mit verbundenen Appliances zu kommunizieren und diese zu steuern, zu analyiseren und zu aktualisieren. Der Starter beinhaltet eine Starter-App, mit der Sie simulierte Appliances erstellen und steuern können, sowie ein Beispiel einer mobilen App, mit dem Sie diese Appliances über Ihr Mobilgerät steuern können.
{:shortdesc}

## Vorbemerkungen

Bevor Sie starten, müssen Sie eine Instanz von {{site.data.keyword.iotelectronics}} in Ihrer {{site.data.keyword.Bluemix_notm}}-Organisation
 bereitstellen. Durch die Bereitstellung einer Instanz werden die Komponentenanwendungen und Services des Starters automatisch bereitgestellt.

 Der [{{site.data.keyword.iotelectronics}}-Starter befindet sich](https://console.{DomainName}/catalog/starters/iot-for-electronics-starter/) im Abschnitt 'Boilerplates' des {{site.data.keyword.Bluemix_notm}}-Katalogs.

## Einführung in {{site.data.keyword.iotelectronics}}
Führen Sie die folgenden Tasks aus, um mit der Nutzung zu beginnen:

1. [Mobile Kommunikation und Sicherheit aktivieren](iotelectronics_config_mca.html) durch Konfigurieren von {{site.data.keyword.amafull}}.
2. [Erstellen simulierter Appliances](iot4ecreatingappliances.html), und zwar mithilfe der {{site.data.keyword.iotelectronics}}-Starter-Webanwendung. Zu Demonstrationszwecken werden Waschmaschinen als simulierte Appliances für den {{site.data.keyword.iotelectronics}}-Starter verwendet. Die von Ihnen zur Herstellung einer Verbindung ausgewählte Appliance kann ein beliebiger Typ von intelligentem Elektronikgerät sein.
3. [Herunterladen des Beispiels für die mobile App herunter und Verbindung zu dieser App herstellen](iotelectronics_config_mobile.html).


## Weitere Schritte
Hier finden Sie Informationen dazu, wie Sie {{site.data.keyword.iotelectronics}} einsetzen können.

- [Erkunden Sie die Starter-App](iot4ecreatingappliances.html), um einen Eindruck davon zu bekommen, wie ein EM (Enterprise Manufacturer) Appliances überwachen kann, die mit {{site.data.keyword.iot_short_notm}} verbunden sind.
- [Erkunden Sie das Beispiel für eine mobile App](iotelectronics_config_mobile.html), um einen Eindruck davon zu bekommen, wie Appliance-Eigner ihre Appliances registrieren und mit diesen interagieren können.
- [Erkunden und verwalten Sie Daten](iotelectronics_dashboard.html) für Ihre registrierten Appliances in {{site.data.keyword.iot_short_notm}}.
- [Erkunden Sie die APIs ![Symbol für externen Link](../../icons/launch-glyph.svg)](http://ibmiotforelectronics.mybluemix.net/public/iot4eregistrationapi.html){:new_window}, um zu sehen, wie Sie Ihre eigenen {{site.data.keyword.iotelectronics}}-Apps anpassen und erweitern können.

# Zugehörige Links
{: #rellinks}
<!-- Related Links last updated 23 October 2016 - new API source -->
## API-Dokumentation
{: #api}
* [{{site.data.keyword.iotelectronics}}-API ![Symbol für externen Link](../../icons/launch-glyph.svg)](https://broker-uss-iot4e.electronics.internetofthings.ibmcloud.com/public/iot4eregistrationapi.html){:new_window}
* [{{site.data.keyword.iot_short}}-API ![Symbol für externen Link](../../icons/launch-glyph.svg)](https://developer.ibm.com/iotfoundation/recipes/api-documentation/){:new_window}


## Komponenten
{: #general}

* [{{site.data.keyword.iotelectronics}}-Dokumentation](iotelectronics_overview.html){:new_window}
* [{{site.data.keyword.iot_full}}-Dokumentation](https://console.ng.bluemix.net/docs/services/IoT/index.html){:new_window}
*  [{{site.data.keyword.amashort}}-Dokumentation](https://console.ng.bluemix.net/docs/services/mobileaccess/overview.html){:new_window}
* [{{site.data.keyword.sdk4nodefull}}-Dokumentation](https://console.ng.bluemix.net/docs/runtimes/nodejs/index.html#nodejs_runtime){:new_window}

## Beispiele
{: #samples}
* [Beispiel für mobile App](https://console.ng.bluemix.net/docs/starters/IotElectronics/iotelectronics_config_mobile.html){:new_window}
