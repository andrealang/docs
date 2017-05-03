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

# Criando acionadores e regras
{: #openwhisk_triggers}

Acionadores e regras do {{site.data.keyword.openwhisk_short}} trazem recursos acionados por eventos para a plataforma. Eventos de origens de eventos externos e internos são canalizados por meio de um acionador e as regras permitem que suas ações reajam a esses eventos.
{: shortdesc}

## Criando Acionadores
{: #openwhisk_triggers_create}

Os acionadores são um canal denominado para uma classe de eventos. A seguir estão exemplos de acionadores:
- Um acionador de eventos de atualização de local.
- Um acionador de uploads de documentos para um website.
- Um acionador de e-mails recebidos.

Acionadores podem ser *disparados* (ativados) usando um dicionário de pares de valores de chaves. Às vezes, esse dicionário é referido como o *evento*. Como com ações, cada disparo de um acionador resulta em um ID de ativação.

Os acionadores podem ser explicitamente disparados por um usuário ou disparados em nome de um usuário por uma origem de eventos externos.
Um *feed* é uma maneira conveniente de configurar uma origem de eventos externos para disparar eventos acionadores que podem ser consumidos pelo {{site.data.keyword.openwhisk_short}}. Exemplos de feeds incluem o seguinte:
- Feed de mudança de dados do Cloudant que dispara um evento acionador toda vez que um documento de um banco de dados é incluído ou modificado.
- Um feed Git que dispara um evento acionador para cada confirmação em um repositório Git.

## Utilizando Regras
{: #openwhisk_rules_use}

Uma regra associa um acionador a uma ação, com cada disparo do acionador fazendo com que a ação correspondente seja chamada com o evento acionador como entrada.

Com o conjunto apropriado de regras, é possível que um único evento acionador chame várias ações ou que uma ação seja chamada como uma resposta a eventos de vários acionadores.

Por exemplo, considere um sistema com as ações a seguir:
- A ação `classifyImage` que detecta os objetos em uma imagem e os classifica.
- A ação `thumbnailImage` que cria uma versão miniatura de uma imagem.

Além disso, suponhamos que haja duas origens de eventos que estejam disparando os acionadores a seguir:
- O acionador `newTweet` que é disparado quando um novo tweet é postado.
- O acionador `imageUpload` que é disparado quando uma imagem é transferida por upload para um website.

É possível configurar regras para que um único evento acionador chame várias ações e fazer vários acionadores chamarem a mesma ação:
- Regra `newTweet -> classifyImage`.
- Regra `imageUpload -> classifyImage`.
- Regra `imageUpload -> thumbnailImage`.

As três regras estabelecem o comportamento a seguir: as imagens em ambos os tweets e as imagens transferidas por upload são classificadas, as imagens transferidas por upload são classificadas e uma versão miniatura é gerada.

## Criando e disparando acionadores
{: #openwhisk_triggers_fire}

Os acionadores podem ser disparados quando determinados eventos ocorrem ou podem ser disparados manualmente.

Como um exemplo, crie um acionador para enviar atualizações de local do usuário e dispare o acionador manualmente.

1. Insira o comando a seguir para criar o acionador:

  ```
  wsk trigger create locationUpdate
  ```
  {: pre}
  ```
  ok: acionador locationUpdate criado
  ```

2. Verifique se você criou o acionador listando o conjunto de acionadores.

  ```
  wsk trigger list
  ```
  {: pre}
  ```
  acionadores
  /someNamespace/locationUpdate                            privado
  ```

  Até o momento, você criou um "canal" denominado para o qual os eventos podem ser disparados.

3. Em seguida, dispare um evento especificando o nome e os parâmetros do acionador:

  ```
  wsk trigger fire locationUpdate --param name Donald --param place "Washington, D.C."
  ```
  {: pre}
  ```
  ok: locationUpdate acionado com id fa495d1223a2408b999c3e0ca73b2677
  ```

Um acionador que é disparado sem uma regra que acompanha para fazer a correspondência não tem efeito visível.
Acionadores não podem ser criados dentro de um pacote; eles devem ser criados diretamente sob um namespace.

## Associando acionadores e ações usando regras
{: #openwhisk_rules_assoc}

As regras são usadas para associar um acionador a uma ação. Toda vez que um evento acionador é disparado, a ação é chamada com os parâmetros de evento.

Como um exemplo, crie uma regra que chame a ação hello sempre que uma atualização de local for postada.

1. Crie um arquivo 'hello.js' com o código de ação que iremos usar:
  ```javascript
  function main(params) {
     return {payload:  'Hello, ' + params.name + ' from ' + params.place};
  }
  ```
  {: codeblock}

2. Certifique-se de que o acionador e a ação existam.
  ```
  wsk trigger update locationUpdate
  ```
  {: pre}
  ```
  wsk action update hello hello.js
  ```
  {: pre}

3. Crie a regra. Observe que a regra será ativada no momento da criação, o que significa que ela estará disponível imediatamente para responder às ativações de seu acionador. Os três parâmetros são o nome da regra, o acionador e a ação.
  ```
  wsk rule create myRule locationUpdate hello
  ```
  {: pre}

  A qualquer momento, é possível escolher desativar uma regra.
  ```
  wsk rule disable myRule
  ```
  {: pre}

4. Dispare o acionador locationUpdate. Toda vez que você disparar um evento, a
ação hello será chamada com os parâmetros do evento.
  ```
  wsk trigger fire locationUpdate --param name Donald --param place "Washington, D.C."
  ```
  {: pre}
  ```
  ok: locationUpdate acionado com id d5583d8e2d754b518a9fe6914e6ffb1e
  ```

5. Verifique se a ação foi chamada, verificando a ativação mais recente.
  ```
  wsk activation list --limit 1 hello
  ```
  {: pre}
  ```
  ativações
  9c98a083b924426d8b26b5f41c5ebc0d             hello
  ```
  ```
  wsk activation result 9c98a083b924426d8b26b5f41c5ebc0d
  ```
  {: pre}
  ```json
     {
     "payload": "Hello, Donald from Washington, D.C."
  }
  ```

  Você vê que a ação hello recebeu a carga útil do evento e retornou a sequência esperada.

É possível criar várias regras que associem o mesmo acionador a diferentes ações.
Acionadores e regras não podem pertencer a um pacote. No entanto, a regra pode ser associada
com uma ação que pertença a um pacote, por exemplo:
  ```
  wsk rule create recordLocation locationUpdate /whisk.system/utils/echo
  ```
  {: pre}

Também é possível usar regras com sequências. Por exemplo, é possível criar uma sequência
de ações `recordLocationAndHello` que é ativada pela regra `anotherRule`.
  ```
  wsk action create recordLocationAndHello --sequence /whisk.system/utils/echo,hello
  ```
  {: pre}
  ```
  wsk rule create anotherRule locationUpdate recordLocationAndHello
  ```
  {: pre}
