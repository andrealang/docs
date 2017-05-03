---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-07"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

<!-- Note to writers - index.md and iot4egettingstarted.md are (almost) duplicates and a change to one should be made to both. index.md appears within the product app as the getting started page. iot4egettingstarted.md appears as the top level topic in the docs toc. -->

# Creating apps with the {{site.data.keyword.iotelectronics}} starter

{{site.data.keyword.iotelectronics_full}} is an integrated, end-to-end solution that enables your apps to communicate with, control, analyze, and update connected appliances. The starter includes a starter app that you can use to create simulated appliances and a sample mobile app that you can use to control those appliances from your mobile device.
{:shortdesc}

## Before you begin

Before you begin, you must deploy an instance of the {{site.data.keyword.iotelectronics}} in your {{site.data.keyword.Bluemix_notm}}
 organization. Deploying an instance automatically deploys the component applications and services of the starter.

 You can [find the {{site.data.keyword.iotelectronics}} starter](https://console.{DomainName}/catalog/starters/iot-for-electronics-starter/) in the Boilerplates section of the {{site.data.keyword.Bluemix_notm}} catalog.

## Getting started with {{site.data.keyword.iotelectronics}}
To get started, complete the following tasks:

1. [Create simulated appliances](iot4ecreatingappliances.html) by using the {{site.data.keyword.iotelectronics}} starter web application. For the purposes of demonstration, washers are used as the simulated appliance within the {{site.data.keyword.iotelectronics}} starter. The appliance that you choose to connect could be any type of smart electronics device.
2. (Optional) [Configure mobile login options with {{site.data.keyword.appid_full}}](https://console.ng.bluemix.net/docs/services/appid/index.html). You can customize the appearance of the login screen that is presented in the mobile app. You can also optionally enable or disable the use of social login credentials. By default, {{site.data.keyword.appid_short_notm}} enables authorization by Facebook and Google+, and mobile app users can use their own social credentials, or they can skip the login process and try the app without logging in.
3. [Download and connect](iotelectronics_config_mobile.html) the sample mobile app.


## What's next
See what you can do with {{site.data.keyword.iotelectronics}}.

- [Explore the starter app](iot4ecreatingappliances.html) to experience how an enterprise manufacturer can monitor appliances that are connected to the {{site.data.keyword.iot_short_notm}}.
- [Explore the sample mobile app](iotelectronics_config_mobile.html) to experience how appliance owners can register and interact with their appliances.
- [Explore and manage data](iotelectronics_dashboard.html) for your registered appliances in {{site.data.keyword.iot_short_notm}}.
- [Explore the APIs ![External link icon](../../icons/launch-glyph.svg)](http://ibmiotforelectronics.mybluemix.net/public/iot4eregistrationapi.html){:new_window} to see how you can customize and expand your own {{site.data.keyword.iotelectronics}} apps.
