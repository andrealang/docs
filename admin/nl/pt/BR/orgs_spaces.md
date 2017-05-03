---



copyright:

  years: 2015, 2016
lastupdated: "2016-12-05"  


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Gerenciando organizações e espaços
{: #orgsspacesusers}

Como um proprietário da conta, é possível gerenciar suas organizações acessando a página **Gerenciar organizações**. Gerenciadores de organização também podem usar a página Gerenciar Organizações,
para gerenciar quaisquer organizações na qual eles estão configurados como o gerente.
{:shortdesc}

Tarefas de gerenciamento incluem o seguinte:

* Criar uma organização ou um espaço
* Renomear uma organização
* Excluir uma organização ou um espaço existente
* Listar os membros da equipe incluídos em sua conta ou organização
* Gerenciar ou visualizar a cota
* Gerenciar domínios customizados

**Observação**: deve-se ser o proprietário de uma conta pay-as-you-go para criar uma organização.

## Organizações
{: #orginfo}

As organizações podem abranger múltiplas regiões e elas são definidas pelos itens a seguir:

<dl>
<dt>Os membros da equipe</dt>
<dd>A função com permissão básica em organizações e espaços. Você deve estar designado a
uma organização para poder receber permissões para os espaços dentro da organização. Para
obter informações detalhadas, veja
[Usuários e funções](users_roles.html#userrolesinfo).</dd>
<dt>Domínios</dt>
<dd>Fornecem a rota na Internet que é alocada para a organização. Uma rota tem um subdomínio e um domínio. Um subdomínio normalmente é o nome do aplicativo. Um
domínio pode ser um domínio do sistema ou um domínio customizado que você registrou para
seu aplicativo. Veja [Gerenciando domínios customizados](orgs_spaces.html#managedomains).<br/>
<p>**Nota**: Se um domínio customizado for incluído, deve-se configurar seu servidor DNS para resolver seu domínio customizado para apontar para o domínio de sistema {{site.data.keyword.Bluemix_notm}}. Dessa
maneira, quando o
{{site.data.keyword.Bluemix_notm}}
receber uma solicitação para o domínio customizado, ele poderá roteá-lo corretamente
para o aplicativo.</p></dd>
<dt>Cota</dt>
<dd>Representa os limites de recurso para a organização, incluindo o número de serviços e a quantia de memória
que pode ser alocada para uso pela organização. As cotas são designadas quando as organizações são criadas. Qualquer
aplicativo ou serviço em um espaço da organização contribui para o uso da cota. A cota não é um valor máximo aplicado. Em vez disso, é um acionador para notificações de gastos. Com planos de Pagamento por uso ou de Assinatura, é possível ajustar a sua cota para aplicativos e contêineres do Cloud Foundry
conforme as necessidades de mudança da sua organização. Consulte [Gerenciando cota](orgs_spaces.html#managequota).</dd>
</dl>

No {{site.data.keyword.Bluemix_notm}}, é possível usar organizações para permitir a colaboração entre membros da equipe e para facilitar o agrupamento lógico de recursos do projeto das
seguintes maneiras:

<ul>
<li>É possível agrupar um conjunto de espaços, aplicativos, serviços, domínios, rotas e membros da equipe juntos em organizações.</li>
<li>É possível gerenciar o acesso aos espaços e organizações por usuário.</li>
</ul>

Ao
criar uma organização, o nome da organização deve ser exclusivo no {{site.data.keyword.Bluemix_notm}}. Se o nome da organização já estiver em uso por outro usuário do
{{site.data.keyword.Bluemix_notm}} Public, Dedicated ou
Local, então, deverá especificar um novo nome. Depois de criar a organização, você será designado automaticamente com a permissão de
*Gerenciador de organização*, que permite editar o nome da organização, incluir membros da equipe e criar ou excluir espaços na organização.

Deve-se entrar em contato com o [Suporte do {{site.data.keyword.Bluemix_notm}} ![Ícone de link externo](../icons/launch-glyph.svg)](http://ibm.biz/bluemixsupport){: new_window} para excluir uma organização. Ao solicitar que
a equipe de suporte exclua uma organização, todos os espaços, aplicativos e serviços dentro da organização são excluídos.

As [funções de usuário](/docs/admin/users_roles.html#userrolesinfo) a seguir podem ser designadas para membros da equipe em uma organização:

<ul>
<li>Gerente da organização</li>
<li>Gerente de faturamento da organização</li>
<li>Auditor da organização</li>
</ul>

<!-- Add info on Manage infrastructure option under a space -->

## Espaços
{: #spaceinfo}

Dentro de uma organização, é possível usar espaços para agrupar um conjunto de aplicativos, serviços e membros da equipe. Espaços são ligados a uma região específica no
{{site.data.keyword.Bluemix_notm}}.

Após incluir membros da equipe em uma organização, é possível conceder a eles permissões para os espaços. Semelhantes às organizações, os espaços também têm um conjunto de
[funções de usuário](/docs/admin/users_roles.html#userrolesinfo) com permissões específicas que são designadas a membros da equipe:

<ul>
<li>Gerente de espaço</li>
<li>Desenvolvedor de espaço</li>
<li>Auditor de espaço</li>
</ul>

**Nota**: um membro da equipe deve ser designado a pelo menos uma das permissões no espaço.

## Criando organizações e espaços
{: #createorg}

Somente proprietários da conta com contas de Pagamento por uso podem criar uma organização. É possível criar uma organização concluindo as etapas a seguir:

1. Clique na página **Conta** &gt; **Gerenciar organizações**.
2. Clique em **Incluir uma nova organização**.
3. Insira o nome da organização.
4. Clique em ** Adicionar**.

É possível criar espaços em
sua organização, por exemplo, um espaço *dev* como
um ambiente de desenvolvimento, um espaço *test* como um ambiente
de teste e um espaço *production* como um ambiente de
produção. Em seguida, é possível associar os apps aos espaços. Conclua as etapas a seguir para criar um espaço:

1. Clique na página **Conta** &gt; **Gerenciar organizações**.
2. Identifique a organização na qual você deseja incluir um
espaço e selecione **Visualizar detalhes**.
4. Clique em **Incluir um espaço**.
5. Insira o nome de espaço.
6. Clique em ** Adicionar**.

## Renomear uma organização
{: #orgrename}

Conclua as etapas a seguir para renomear sua organização:

1. Clique na página **Conta** &gt; **Gerenciar organizações**.
2. Identifique a organização que deseja editar e selecione **Visualizar detalhes**.
3. Selecione **Editar organização**.
4. Selecione **Editar** para o título da organização.
5. Digite o novo nome da organização.
6. Clique em **SALVAR**.

## Excluir uma organização ou um espaço existente
{: #deleteorgs}

Como o proprietário da conta, é possível entrar em contato com o [Suporte do {{site.data.keyword.Bluemix_notm}} ![Ícone de link externo](../icons/launch-glyph.svg)](http://ibm.biz/bluemixsupport){: new_window} para excluir uma organização. 

**Nota**: Não é possível inverter operações de exclusão. Você perderá todos os aplicativos e
serviços que estiverem associados à organização.

É possível excluir um espaço da página **Gerenciar organizações**:

1. Clique na página **Conta** &gt; **Gerenciar organizações**.
2. Identifique a organização que deseja editar e selecione **Visualizar detalhes**.
3. Identifique o espaço que você deseja excluir e selecione **Editar espaço**.
4. Clique em **Excluir espaço**.

## Listando membros
{: #listmembers}

Conclua as etapas a seguir, para listar os membros para uma organização específica:

1. Clique na página **Conta** &gt; **Gerenciar organizações**.
2. Identifique a organização para a qual deseja visualizar os membros e clique em **Visualizar detalhes**.
3. Clique em **Editar organização**.
4. É possível ver os membros de sua organização e suas funções na guia **USUÁRIOS**.

Conclua as etapas a seguir, para listar os membros para um espaço específico:

1. Clique na página **Conta** &gt; **Gerenciar organizações**.
2. Identifique a organização para a qual deseja visualizar os membros e clique em **Visualizar detalhes**.
3. Identifique o espaço para a qual deseja visualizar os membros e clique em **Editar espaço**.
4. É possível ver os membros de seu espaço e suas funções na guia **USUÁRIOS**.

## Gerenciando cota
{: #managequota}

Como um proprietário da conta ou gerenciador de organização do {{site.data.keyword.Bluemix_notm}}, é possível visualizar a cota usada e alocada para uma
organização. A cota representa os limites de recurso para a organização, a qual é designada quando a organização é criada. O limite não é um valor máximo aplicado com relação à organização. Em vez disso, é um acionador para notificações de gastos. Dependendo se você tem uma conta de avaliação
ou uma conta faturável, os recursos que estão disponíveis para uma organização variam. Qualquer aplicativo ou serviço em um espaço dentro da organização contribui
para o uso da cota alocada.

Para visualizar a cota usada e alocada para uma organização, conclua as etapas a seguir:

1. Clique na página **Conta** &gt; **Gerenciar organizações**.
2. Identifique a organização para a qual deseja visualizar a cota e clique em **Visualizar detalhes**.
3. Clique em **Editar organização**.
4. Se você tiver espaços definidos em mais de uma região, selecione a região específica que deseja visualizar.
5. Clique em **COTA**. 
6. Por padrão, a página de cota do **Cloud Foundry** é aberta. É possível visualizar os detalhes da cota para os recursos a seguir:
 * MEMÓRIA
 * SERVIÇOS
 * PLANO
 * PREÇO
7. Clique em **Contêineres** para visualizar a alocação de cota de contêiner usada e disponível. A alocação de contêiner varia dependendo
de seu plano de precificação. É possível visualizar os detalhes da cota para os recursos a seguir:
 * MEMÓRIA
 * IP PÚBLICO

**Nota:** Os contêineres não estão disponíveis na região de Sydney do {{site.data.keyword.Bluemix_notm}}. 

Para obter mais informações sobre contêineres, consulte [Cota](/docs/containers/container_planning_org_ov.html#container_planning_quota) na
documentação de Contêineres.
Para mudar a cota que está alocada para uma organização, deve-se abrir um chamado de suporte. Para obter mais informações sobre como abrir um chamado de suporte,
consulte [Obtendo suporte ao cliente](/docs/support/index.html#contacting-support). 

## Gerenciando Domínios
{: #managedomains}

Como um proprietário da conta ou gerenciador de organização, é possível visualizar o domínio do sistema e incluir domínios customizados para aplicativos que são construídos dentro de uma organização e
de seus espaços. Como um gerenciador de espaço, a guia **Domínios** para um espaço é uma lista somente leitura dos domínios designados ao espaço. 

1. Clique na página **Conta** &gt; **Gerenciar organizações**.
2. Identifique a organização que você deseja visualizar ou para a qual deseja editar domínios.
3. Selecione **Visualizar detalhes** para essa organização.
4. Clique em **Editar organização**.
5. Clique em **DOMÍNIOS**.

Se você incluir um domínio customizado, deverá
configurar seu servidor DNS para resolver seu domínio customizado para apontar para o
domínio do sistema {{site.data.keyword.Bluemix_notm}}. Dessa
maneira, quando o
{{site.data.keyword.Bluemix_notm}}
receber uma solicitação para o domínio customizado, ele poderá roteá-lo corretamente
para o aplicativo. O domínio do sistema está sempre disponível para um espaço e domínios customizados também podem ser alocados para um espaço. Aplicativos criados em um espaço podem usar qualquer um dos
domínios listados para esse espaço. Para obter mais informações sobre como criar e usar domínios customizados, consulte [Usando um domínio customizado](/docs/manageapps/updapps.html#domain).
