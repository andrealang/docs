---

copyright:
  years: 2016
lastupdated: "2017-04-08"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Getting started with Compose for Redis
{: #getting-started-with-compose-for-redis}

Redis is an open source, in-memory, key-value store. Values in Redis can be simple strings, hashes, lists, and sets or powerful bitmaps, hyperloglogs, and geospatial indexes. Redis is ideal as an application cache or quick response data store. {{site.data.keyword.composeForRedis_full}} gives you a configuration that is pre-tuned for high availability and on-disk persistence, all locked down with extra security features.
{:shortdesc}

**Note:** Any Compose service instances that were provisioned before 14 September 2016 that are still active can still be used and directly accessed at [https://www.compose.com/](https://www.compose.com). Any Compose service instance that is provisioned from this point forward is directly accessed and used within your Bluemix account.

Complete these steps to get started with {{site.data.keyword.composeForRedis}}.

1. [Create a {{site.data.keyword.composeForRedis}} instance](https://console.ng.bluemix.net/catalog/services/compose-for-redis/).

  When you create an instance of the service, ensure that you choose both a name for your service and a credential name. Leave the service unbound; you can connect an application to your service later by using the credentials that are provided when the service is provisioned. The various credential values are listed in the *Available credentials* section.

2. Connect to your {{site.data.keyword.composeForRedis}} service.

  To connect an app to your service, use the credentials that are created along with the service. The sample app demonstrates how to use Node.js to connect to a {{site.data.keyword.composeForRedis}} service.

  Download the [compose-redis-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-redis-helloworld-nodejs) sample app and follow the instructions in the readme file. Then, in your application details page in Bluemix, click **View APP**.

## Available credentials

Field Name|Description
----------|-----------
`uri`|The URI to be used when connecting to the service, which includes the schema (redis:), admin user name and password, the host name of the server and the port number to connect to.
`uri_cli`|A `redis-cli` command line that connects to the database instance.
`deployment_id`|An internal identifier for the service as created within Compose.
`db_type`|The type of database that is offered by the service; in this case `redis`.
`name`|The database deployment name.
{: caption="Table 1. {{site.data.keyword.composeForRedis}} credentials" caption-side="top"}

# Related Links
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Compose Articles](https://www.compose.com/articles/){:new_window}

## Tutorials and Samples
{: #samples}
* [compose-redis-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-redis-helloworld-nodejs){:new_window}

## Related Links
{: #general}
* [Compose Help](https://help.compose.com/docs){:new_window}
