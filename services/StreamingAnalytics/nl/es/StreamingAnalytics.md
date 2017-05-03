---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Acerca de
{: #about}

Puede realizar análisis en tiempo real sobre los datos en movimiento como parte de las aplicaciones de {{site.data.keyword.Bluemix_short}} utilizando {{site.data.keyword.streaminganalyticsfull}}. 
{:shortdesc}

{{site.data.keyword.streaminganalyticsshort}} está basado en {{site.data.keyword.streamsshort}}, una plataforma analítica avanzada que se puede utilizar para introducir, analizar y correlacionar información a medida que llega desde distintos tipos de orígenes de datos en tiempo real. Cuando se crea una instancia del servicio {{site.data.keyword.streaminganalyticsshort}}, se obtiene una instancia propia de {{site.data.keyword.streamsshort}} que se ejecuta en la nube de {{site.data.keyword.Bluemix_short}}, lista para ejecutarse en las aplicaciones de {{site.data.keyword.streamsshort}}.

¿Es nuevo en {{site.data.keyword.streaminganalyticsshort}}? Obtenga una [rápida presentación del servicio](https://developer.ibm.com/streamsdev/docs/streaming-analytics-now-available-bluemix-2/){:new_window}. Si desea profundizar en el uso de sus propias aplicaciones, es necesario un entorno de desarrollo de {{site.data.keyword.streamsshort}} y preparar su SPL para la nube.

El servicio de {{site.data.keyword.streaminganalyticsshort}} proporciona las siguientes capacidades para permitirle desplegar, analizar y supervisar datos en la nube:

**Uso interactivo y programático del servicio:**

Puede utilizar el servicio de forma interactiva a través de la [consola de {{site.data.keyword.streaminganalyticsshort}}](/docs/services/StreamingAnalytics/c_streams_console.html) o mediante programación a través de la [API REST de {{site.data.keyword.streaminganalyticsshort}}](https://console.ng.bluemix.net/apidocs/220){:new_window}.

**Despliegue y supervisión de las aplicaciones de SPL y Java:**

{{site.data.keyword.streamsfull}} Processing Language (SPL) es un lenguaje de programación que se utiliza para crear aplicaciones de procesamiento de secuencias. Puede escribir aplicaciones de {{site.data.keyword.streamsshort}} en SPL o en Java. [Desplegar y supervisar estas aplicaciones](/docs/services/StreamingAnalytics/t_deploytocloud.html) mediante {{site.data.keyword.streaminganalyticsshort}}. 

**Compatibilidad con los operadores de {{site.data.keyword.streamsshort}}:**

Los operadores de {{site.data.keyword.streamsshort}} del [kit de herramientas estándar de {{site.data.keyword.streamsshort}} Processing Language (SPL) deben ser compatibles](/docs/services/StreamingAnalytics/c_beta_adapters.html) con {{site.data.keyword.streaminganalyticsshort}}.

## Responsabilidades de {{site.data.keyword.streaminganalyticsfull}}

### Responsabilidades del cliente

El cliente es responsable de:

* Seguir la configuración inicial de IBM de {{site.data.keyword.streamsshort}} y de supervisar, configurar y gestionar los trabajos de {{site.data.keyword.streamsshort}} que se ejecutan en la instancia. El cliente tiene flexibilidad para iniciar y detener la instancia e iniciar y detener jobskeywordnning en la instancia.
* Desarrollar, según sea necesario, programas y aplicaciones en el servicio para analizar datos y obtener detalles de los mismos. El cliente también es responsable de la calidad y el rendimiento de dichos programas o aplicaciones desarrollados. Los programas se pueden desarrollar en SPL, Java o en otros lenguajes soportados mediante la característica Topology de {{site.data.keyword.streamsshort}}. Se deben compilar con {{site.data.keyword.streamsshort}} Developer Edition o {{site.data.keyword.streamsshort}} Quick Start Edition con el mismo sistema operativo que se ha utilizado para {{site.data.keyword.streaminganalyticsshort}}. 
* Comprobar periódicamente el siguiente enlace para estar informado sobre tiempos de inactividad disruptivos o no disruptivos planificados - [https://developer.ibm.com/bluemix/support/#status](https://developer.ibm.com/bluemix/support/#status){:new_window}  
* Hacer copia de seguridad de todos los datos, metadatos, archivos de configuración y parámetros de entorno según los requisitos de la empresa para garantizar la continuidad.
* Restaurar los datos, metadatos, archivos de configuración y parámetros de entorno de una copia de seguridad para garantizar la continuidad, en el caso de que se produzca un error de cualquier tipo, incluidos, aunque sin limitarse a los mismos, errores en el centro de datos o de pod, errores del servidor, errores del disco duro o errores de software.

### Responsabilidades de IBM

Como parte de {{site.data.keyword.streaminganalyticsfull}}, IBM:

* Proporcionará y gestionará servidores, almacenamiento e infraestructura de red para la instancia del cliente. 
* Proporcionará una configuración inicial de {{site.data.keyword.streamsshort}} en los nodos seleccionados.
* Proporcionará y gestionará la infraestructura para disponer de Internet y de un cortafuegos interno para garantizar la protección y aislamiento. 
* Supervisará y gestionará los siguientes componentes en {{site.data.keyword.streaminganalyticsfull}}:
	* Componentes de red
	* Servidores y su almacenamiento local
	* Sistemas operativos de la infraestructura
	* Servicios de gestión de {{site.data.keyword.streamsshort}}
	* Instancias de {{site.data.keyword.streamsshort}} 
* Proporcionará partes de mantenimiento, incluidos los parches de seguridad necesarios para los sistemas operativos de la infraestructura y para {{site.data.keyword.streamsshort}}.
* Realizará tareas de mantenimiento que no deberían derivar en inactividad del sistema (mantenimiento “no disruptivo”) y mantenimiento que requiera cierto tiempo de inactividad y reinicio (mantenimiento “disruptivo””), que se llevarán a cabo en momentos planificados que se publicarán en [https://developer.ibm.com/bluemix/support/#status](https://developer.ibm.com/bluemix/support/#status){:new_window} 
* Cualquier cambio en los tiempos planificados de mantenimiento se publicará con el aviso adecuado. 
