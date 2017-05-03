---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-14"
---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 裝置的 HTTP REST API
{: #api}

**重要事項：**裝置的 {{site.data.keyword.iot_full}} HTTP REST API 特性僅是有限測試版程式的一部分。未來更新可能包含與此特性的目前版本不相容的變更。請試用，並且[讓我們知道您的想法 ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.ibm.com/answers/smart-spaces/17/internet-of-things.html){: new_window}。

## 存取 HTTP REST API 文件
{: #api_link}

若要存取 {{site.data.keyword.iot_short_notm}} HTTP REST API 文件，以及取得如何將裝置整合至組織中的相關資訊，請參閱 [API](../reference/api.html)。

唯一支援的 {{site.data.keyword.iot_short_notm}} HTTP REST API 版本是第 2 版。請確定您的 {{site.data.keyword.iot_short_notm}} 解決方案使用的是第 2 版。

## 用戶端連線
{: #client_connections}

如需用戶端安全以及如何將用戶端連接至 {{site.data.keyword.iot_short_notm}} 中裝置的相關資訊，請參閱[將應用程式、裝置及閘道連接至 {{site.data.keyword.iot_short_notm}}](../reference/security/connect_devices_apps_gw.html)。

# 裝置的 HTTP REST 傳訊 API
{: #rest_messaging_api}

若要存取「{{site.data.keyword.iot_short_notm}} HTTP 傳訊 API」文件，以及尋找使用 HTTP 來發佈事件的相關資訊，請參閱 [{{site.data.keyword.iot_short_notm}} HTTP 傳訊 API ![外部鏈結圖示](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/http-messaging.html){: new_window}。

## 發佈事件
{: #event_publication}

除了使用 MQTT 傳訊通訊協定之外，您還可以使用 HTTP REST API 指令來配置裝置，讓它透過 HTTP 將事件發佈至 {{site.data.keyword.iot_short_notm}}。

請使用下列其中一個 URL，來提交來自連接至 {{site.data.keyword.iot_short_notm}} 之裝置的 `POST` 要求：

### 未受保護的 POST 要求
<pre class="pre"><code class="hljs">http://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>

### 安全的 POST 要求

<pre class="pre"><code class="hljs">https://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:8883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>

**附註：**您也可以指定埠 443（預設 SSL 埠）來進行安全 HTTP API 呼叫。

如果您要將裝置或應用程式連接至 Quickstart 服務，請改用下列其中一個 URL：

### 連接至 Quickstart 的未受保護 POST 要求
<pre class="pre"><code class="hljs">http://quickstart.messaging.internetofthings.ibmcloud.com:1883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>

### 連接至 Quickstart 的安全 POST 要求
<pre class="pre"><code class="hljs">https://quickstart.messaging.internetofthings.ibmcloud.com:8883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>

**重要注意事項：**
- 在現行 HTTP REST API 版本中，您只能使用 HTTP 傳訊來提交裝置事件。使用 MQTT 傳訊通訊協定，以提交其他裝置管理及控制特性的要求。
- 因為無法變更授權 HTTP 標頭，所以只能重複使用 HTTP 連線來發佈相同裝置的事件。
- 您也可以指定埠 443（預設 SSL 埠）來進行安全 HTTP API 呼叫。

### 鑑別

所有要求都必須包含授權標頭。基本鑑別是唯一支援的方法。裝置透過 {{site.data.keyword.iot_short_notm}} HTTP REST API 提出 HTTP 要求時，需要下列認證：

|認證|必要輸入|
|:---|:---|
|使用者名稱|`use-token-auth`
|密碼| 在登錄裝置時自動產生或手動指定的鑑別記號。


### Content-Type 要求標頭

`Content-Type` 要求標頭必須隨要求提供。下表顯示支援的類型如何對映至 {{site.data.keyword.iot_short_notm}} 內部格式。

|Content-Type 標頭|{{site.data.keyword.iot_short_notm}} 中的格式|
|:---|:---|
|text/plain|"text"
|application/json| "json"
|application/xml | "xml"
|application/octet-stream|"bin"

### 服務品質

與 MQTT 服務品質「最多一次」遞送服務水準 0 類似，HTTP REST 傳訊提供非持續訊息遞送，但會驗證要求正確無誤，並驗證要求會先遞送至伺服器，再傳送 HTTP 回應。包含 HTTP 狀態碼 200 的回覆會確認已將訊息遞送至伺服器。當您使用「最多一次」的 MQTT 服務品質水準或 HTTP 對等項目來遞送事件訊息時，裝置或應用程式必須實作重試邏輯以保證遞送。

如需 {{site.data.keyword.iot_short_notm}} 的 MQTT 通訊協定及服務品質水準的相關資訊，請參閱 [MQTT 傳訊](../reference/mqtt/index.html)。

## 前次事件快取
{: #last-event-cache}

您可以使用 {{site.data.keyword.iot_short_notm}} 的「前次事件快取 API」，擷取裝置前次傳送的事件。不論裝置是連線還是離線，此作業皆可運作，如此可讓您擷取裝置狀態，而不管裝置的實體位置或使用狀態。您可以擷取特定裝置之事件 ID 的前次記錄值，或特定裝置所報告之每一個事件 ID 的前次記錄值。可針對最多 365 天之前發生的任何特定事件，擷取裝置的前次事件資料。

若要要求特定事件 ID 的最新值，請使用下列 API 要求，其會傳回 "power" 事件 ID 的前次記錄值。

```
GET /api/v0002/device/types/<device-type>/devices/<device-id>/events/power
```

傳回的回應具有下列 JSON 格式：

```
{
    "deviceId": "<device-id>",
    "eventId": "power",
    "format": "json",
    "payload": "eyJzdGF0ZSI6Im9uIn0=",
    "timestamp": "2016-03-14T14:12:06.527+0000",
    "typeId": "<device-type>"
}
```

**附註：**API 回應為 JSON 格式時，可以使用任何格式來撰寫事件有效負載。「前次事件快取 API」所傳回的有效負載會使用 base64 進行編碼。

若要要求裝置所報告之每個事件 ID 的最新值，請使用下列 API 要求：

```
GET /api/v0002/device/types/<device-type>/devices/<device-id>/events
```

回應將會包含裝置所傳送的所有事件 ID。在下列範例中，會傳回 "power" 及 "temperature" 事件的值。

```
[
    {
        "deviceId": "<device-id>",
        "eventId": "power",
        "format": "json",
        "payload": "eyJzdGF0ZSI6Im9uIn0=",
        "timestamp": "2016-03-14T14:12:06.527+0000",
        "typeId": "<device-type>"
    },
    {
        "deviceId": "<device-id>",
        "eventId": "temperature",
        "format": "json",
        "payload": "eyJpbnRlcm5hbCI6MjIsICJleHRlcm5hbCI6MTZ9",
        "timestamp": "2016-03-14T14:17:44.891+0000",
        "typeId": "<device-type>"
    }
]
```
