---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 피드 구현
{: #openwhisk_feeds}

{{site.data.keyword.openwhisk_short}}는 개방형 API를 지원하며 여기서 모든 사용자는 **패키지**에 하나의 **피드**로서 이벤트 생성자 서비스를 노출할 수 있습니다. 이 절에서는 사용자 소유의 피드를 제공하기 위한 아키텍처 관련 옵션 및 구현 옵션에 대해 설명합니다. 

이 자료는 본인 소유의 피드를 공개하려는 고급 {{site.data.keyword.openwhisk_short}} 사용자를 대상으로 합니다. 대부분의 {{site.data.keyword.openwhisk_short}} 사용자는 이 절을 건너뛰어도 됩니다.

## 피드 아키텍처

피드를 작성하기 위한 최소 3개의 아키텍처 패턴(**훅**, **폴링** 및 **연결**)이 있습니다. 

### 훅
*훅* 패턴에서는 다른 서비스에서 노출한 [웹훅](https://en.wikipedia.org/wiki/Webhook) 기능을 사용하여 피드를 설정합니다. 이 전략에서는 트리거를 실행하는 URL에 직접 게시하는 외부 서비스에 웹훅을 구성합니다. 이 방법은 지금까지 빈도가 낮은 피드를 구현하는 가장 쉽고 가장 매력적인 옵션입니다.

<!-- The github feed is implemented using webhooks.  Put a link here when we have the open repo ready -->

### 폴링
"폴링" 패턴에서는 새 데이터를 페치하기 위해 엔드포인트를 주기적으로 폴링하는 {{site.data.keyword.openwhisk_short}} *조치*를 준비합니다. 이 패턴은 비교적 빌드하기가 쉽지만, 이벤트 빈도가
폴링 간격에 의해 제한됩니다. 

### 연결
"연결" 패턴에서는 피드 소스와의 지속적 연결을 유지보수하는 별도의 서비스를 어딘가에 준비합니다. 연결 기반 구현은 푸시 알림을 설정하기 위해 또는 장기간의 폴링을 통해 서비스 엔드포인트와 상호작용할 수 있습니다. 

<!-- Our cloudant changes feed is connection based.  Put a link here to
an open repo -->

<!-- What is the foundation for the Message Hub feed? If it is "connections" then lets put a link here as well -->

## 피드와 트리거 사이의 차이점

피드와 트리거는 밀접한 관련이 있지만
기술적으로 개념이 뚜렷이 구분됩니다.    

- {{site.data.keyword.openwhisk_short}}가 시스템에 플로우되는 **이벤트**를 처리합니다.

- **트리거**는 기술적으로 이벤트 클래스의 이름입니다. 각 이벤트는 정확히 하나의 트리거에 속합니다. 유추하면 트리거는 토픽 기반 퍼브-서브 시스템의 *토픽*과
유사합니다. **규칙** *T -> A*는 "트리거 *T*의 이벤트가 도착할 때마다 트리거 페이로드로 조치 *A*를 호출한다"는 의미입니다.

- **피드**는 모두 특정 트리거 *T*에 속하는 이벤트 스트림입니다. 피드는 피드를 구성하는 이벤트 스트림의 작성, 삭제, 일시정지 및 재개를 제어하는 **피드 조치**에 의해 제어됩니다. 피드 조치는 일반적으로 알림을 관리하는 REST API를 통해 이벤트를 생성하는 외부 서비스와 상호작용합니다. 

##  피드 조치 구현

*피드 조치*는 일반 {{site.data.keyword.openwhisk_short}} *조치*이지만 다음 매개변수를 승인해야 합니다.
* **lifecycleEvent**: 'CREATE', 'DELETE', 'PAUSE' 또는 'UNPAUSE' 중 하나입니다.
* **triggerName**: 이 피드에서 생성된 이벤트를 포함하는 트리거의 완전한 이름입니다. 
* **authKey**: 방금 언급한 트리거를 소유하는 {{site.data.keyword.openwhisk_short}} 사용자의 기본 auth 신임 정보입니다.

피드 조치는 피드를 관리하는 데 필요한 다른 매개변수도 승인할 수 있습니다. 예를 들어, cloudant changes 피드 조치는 *'dbname'*, *'username'* 등의 매개변수를 수신할 것으로 예상합니다. 

사용자가 CLI에서 **--feed** 매개변수를 사용하여 트리거를 작성하면 시스템이 적절한 매개변수로 피드 조치를 자동으로 호출합니다. 

예를 들어, 사용자가 사용자 이름 및 비밀번호를 바인드된 매개변수로 사용하여 `cloudant` 패키지에
대한 `mycloudant` 바인딩을 작성했다고 가정하십시오. 사용자가 CLI에서 다음 명령을 실행하는 경우:

`wsk trigger create T --feed mycloudant/changes -p dbName myTable`

시스템은 백그라운드에서 다음과 동등한 조치를 수행합니다. 

`wsk action invoke mycloudant/changes -p lifecycleEvent CREATE -p triggerName T -p authKey <userAuthKey> -p password <password value from mycloudant binding> -p username <username value from mycloudant binding> -p dbName mytype`

*changes*라는 피드 조치는 이러한 매개변수를 사용하며, Cloudant에서 적절한 구성으로 트리거 *T*로 향하는 이벤트 스트림을 설정하는 데 필요한 모든 조치를 수행할 것으로 예상됩니다.     

Cloudant *changes* 피드 조치는 연결 기반 아키텍처로 구현한 *cloudant 트리거* 서비스와 직접 대화합니다. 기타 아키텍처에 대해서는 뒤에서 설명합니다. 

`wsk trigger delete`의 경우 유사한 피드 조치 프로토콜이 발생합니다.     

## 훅을 사용하여 피드 구현

이벤트 생성자가 웹훅/콜백 기능을 지원하면 훅을 통해 피드를 설정하기가 쉽습니다. 

이 방법을 사용하면 OpenWhisk 외부에 지속적 서비스를 준비할 *필요가 없습니다*. 써드파티 웹훅 API와 직접 협상하는 Stateless {{site.data.keyword.openwhisk_short}} *피드 조치*를 통해 모든 피드 관리가 자연적으로 수행됩니다.

`CREATE`를 사용하여 호출하면 피드 조치는 단순히 다른 특정 서비스에 대한 웹훅을 설치하여 해당 원격 서비스에 OpenWhisk의 적절한 `fireTrigger` URL로 알림을 게시하도록 요청합니다. 

웹훅에 다음과 같은 URL로 알림을 전송하도록 지시해야 합니다. 

`POST /namespaces/{namespace}/triggers/{triggerName}`

POST 요청을 포함하는 양식은 트리거 이벤트에서 매개변수를 정의하는 JSON 문서로 해석됩니다.
{{site.data.keyword.openwhisk_short}} 규칙은 이러한 트리거 매개변수를 이벤트의 결과로 실행되는 조치에 전달합니다.

## 폴링을 사용하여 피드 구현

지속적 연결 또는 외부 서비스를 준비할 필요 없이, 전적으로 OpenWhisk 내에서 피드 소스를 폴링하는 {{site.data.keyword.openwhisk_short}} *조치*를 설정할 수 있습니다.

웹훅을 사용할 수 없지만 고볼륨 또는 저지연 응답 시간이 필요하지 않는 피드의 경우, 폴링은 매력적인 옵션입니다. 

폴링 기반 피드를 설정하기 위해 피드 조치는 `CREATE`를 위해 호출될 때 다음 단계를 수행합니다. 

1.   피드 조치가 `whisk.system/alarms` 피드를 사용하여 원하는 빈도를 가진 주기적 트리거(*T*)를 설정합니다. 
2.   피드 개발자가 단순히 원격 서비스를 폴링하고 새 이벤트를 리턴하는 `pollMyService` 조치를 작성합니다. 
3.  피드 조치가 *규칙* *T -> pollMyService*를 설정합니다. 

이 프로시저는 별도의 서비스를 필요로 하지 않고 전적으로 {{site.data.keyword.openwhisk_short}} 조치를 사용하여 폴링 기반 트리거를 구현합니다.

## 연결을 통해 피드 구현

아키텍처와 관련된 앞의 두 선택사항은 단순하고 구현하기가 쉽습니다. 그러나 고성능 피드를 원하는 경우, 지속적 연결 및 장기 폴링을 대체할 기술이나 이와 유사한 기술이 없습니다. 

{{site.data.keyword.openwhisk_short}} 조치는 단기간 실행되어야 하므로 조치가 써드파티와의 지속적 연결을 유지보수할 수 없습니다. 대신 항상 실행되는
별도의 서비스(OpenWhisk 외부의)를 준비해야 합니다. 이를 *제공자 서비스*라고 합니다. 제공자 서비스는 장기 폴링 또는 다른 연결 기반 알림을 지원하는 써드파티 이벤트 소스와의 연결을 유지보수할 수 있습니다. 

제공자 서비스는 {{site.data.keyword.openwhisk_short}} *피드 조치*가 피드를 제어하는 데 필요한 REST API를 제공해야 합니다. 제공자 서비스는 이벤트 제공자와 {{site.data.keyword.openwhisk_short}} 사이의 프록시 역할을 합니다. 써드파티에서 이벤트를 수신하면 트리거를 실행하여 이 이벤트를 {{site.data.keyword.openwhisk_short}}에 전송합니다.

Cloudant *changes* 피드가 대표적인 예입니다. 이 피드는 지속적 연결을 통한 Cloudant 알림과 {{site.data.keyword.openwhisk_short}} 트리거 사이에서 중재하는 `cloudanttrigger` 서비스를 준비합니다.
<!-- TODO: add a reference to the open source implementation -->

*알람* 피드는 유사한 패턴으로 구현됩니다. 

연결 기반 아키텍처는 최고 성능 옵션이지만 폴링 및 훅 아키텍처에 비해 오퍼레이션에 더 많은 오버헤드를 가합니다.   
