---

copyright:
  years: 2015, 2017
lastupdated: "2017-2-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


#Schaltfläche für die Bereitstellung in {{site.data.keyword.Bluemix_notm}} erstellen {: #deploy-button} 

Die Schaltfläche für die Bereitstellung in {{site.data.keyword.Bluemix}} bietet eine effiziente Möglichkeit, die auf Git basierende öffentliche App zu teilen, sodass andere Personen mit dem Code experimentieren und diesen in IBM {{site.data.keyword.Bluemix_notm}} bereitstellen können. Die Schaltfläche erfordert nur minimalen Konfigurationsaufwand und kann überall dort eingefügt werden, wo Markupunterstützung bereitsteht. Jeder, der auf diese Schaltfläche klickt, erstellt eine geklonte Kopie des Codes in einem neuen Git-Repository, sodass die ursprüngliche App unverändert bleibt. 
{: shortdesc} 

**Tipp:** Falls Unternehmensbranding ein wichtiges Thema ist, können Sie in Ihren Inhalt ein [iFrame-Muster 'In {{site.data.keyword.Bluemix_notm}} bereitstellen'](/docs/develop/deploy_button_embed.html) integrieren, statt eine Schaltfläche einzufügen. Wenn Benutzer eine geklonte Kopie Ihrer öffentlichen Git-basierten App erstellen, verbleiben sie in Ihrem Inhalt und werden nicht an die Bluemix-Website 'bluemix.net' weitergeleitet. 

**Hinweis:** Die Toolchains-Funktion ist nun verfügbar. Jeder Benutzer, der auf die Schaltfläche zum Bereitstellen in {{site.data.keyword.Bluemix_notm}} klickt, kann auf den Link im Banner klicken, um zu versuchen, die Anwendung mithilfe einer Toolchain bereitzustellen.

Wenn eine Person auf die Schaltfläche klickt, werden folgende Aktionen ausgeführt: 

1. Wenn die Person nicht über ein aktives {{site.data.keyword.Bluemix_notm}}-Konto verfügt, muss ein Testkonto erstellt werden. 

2. Die Person kann eine Region, eine Organisation, einen Bereich und einen App-Namen auswählen. Der vorgeschlagene App-Name wird aus dem vorherigen App-Namen, dem Benutzernamen der Person und der Uhrzeit erstellt. 

3. Der Master-Zweig des ursprünglichen öffentlichen Git-Repositorys wird in ein neues privates {{site.data.keyword.jazzhub_title}}-Projekt mit einem neuen Git-Repository geklont. 

4. Wenn für die App eine Builddatei benötigt wird, wird die Builddatei automatisch erkannt und die App wird erstellt. 

5. Wenn für den Build- und Bereitstellungsprozess eine Pipeline konfiguriert ist, wird eine Datei mit dem Namen `pipeline.yml` zum Bereitstellen der App verwendet.

6. Wenn für die App ein Container erforderlich ist, werden eine Datei `pipeline.yml`, die den Service **IBM Containers** definiert, sowie eine Dockerfile, die ein Image definiert, für die Bereitstellung der App in einem {{site.data.keyword.Bluemix_notm}}-Container verwendet. 

7. Die App wird in der {{site.data.keyword.Bluemix_notm}}-Organisation der Person bereitgestellt. 

##Beispiele für die Schaltfläche {: #button-examples} 

Beispiel für eine App-Schaltfläche für ein öffentliches {{site.data.keyword.jazzhub_short}}-Repository:

<p>
<a class="xref" href="https://bluemix.net/deploy?repository=https://hub.jazz.net/git/idsorg/sample-java-cloudant" target="_blank" title="(Wird in einer neuen Registerkarte oder in einem neuen Fenster geöffnet)"><img class="image" src="images/deploy_buttonx2.png" alt="In Bluemix bereitstellen" /></a>
</p> 

Beispiel für eine App-Schaltfläche für ein öffentliches GitHub-Repository: 

<p>
<a class="xref" href="https://bluemix.net/deploy?repository=https://github.com/ibmjstart/bluemix-node-mysql-uploader" target="_blank" title="(Wird in einer neuen Registerkarte oder in einem neuen Fenster geöffnet)"><img class="image" src="images/deploy_buttonx2.png" alt="In Bluemix bereitstellen" /></a>
</p> 

Im Folgenden sehen Sie ein Beispiel für eine Schaltfläche für eine in einem {{site.data.keyword.Bluemix_notm}}-Container bereitgestellte App: 

<p>
<a class="xref" href="https://bluemix.net/deploy?repository=https://github.com/Puquios/hello-containers" target="_blank" title="(Wird in einer neuen Registerkarte oder in einem neuen Fenster geöffnet)"><img class="image" src="images/deploy_buttonx2.png" alt="In Bluemix bereitstellen" /></a>
</p> 

##Schaltfläche erstellen {: #create-button}

Gehen Sie wie folgt vor, um eine Schaltfläche für die Bereitstellung in {{site.data.keyword.Bluemix_notm}} zu erstellen: 

<ol>
<li> Kopieren und modifizieren Sie eine der folgenden Snippetvorlagen und schließen Sie ein öffentliches Git-Repository ein.
<p></p>
<p>
<strong>Tipp:</strong> Wenn Sie die Buildeingabe für ein DevOps Services-Projekt angeben wollen, fügen Sie der Git-URL einen Zweigparameter (Branch) hinzu. Wenn Sie einen Zweigparameter hinzufügen, wird das ursprüngliche öffentliche Git-Repository, einschließlich aller Zweige, in ein neues, privates DevOps Services-Projekt mit einem neuen Git-Repository geklont. Der angegebene Git-Zweig wird als Eingabe für den Build-Job festgelegt. Wenn Sie keinen Zweig angeben, wird als Eingabe für den Build-Job standardmäßig der Master-Zweig festgelegt.
</p>
<ul>
<li>HTML:
<p>
Standard-Master-Zweig:
</p>
<pre class="codeblock">
&lt;a href="https://bluemix.net/deploy?repository=&lt;URL des Git-Repositorys>" # [required]&gt;&lt;img src="https://bluemix.net/deploy/button.png" alt="In Bluemix bereitstellen"&gt;&lt;/a&gt;
</pre>
<p>
Angegebener Git-Zweig:
</p>
<pre class="codeblock">
&lt;a href="https://bluemix.net/deploy?repository=&lt;URL des Git-Repositorys&gt;&branch=&lt;Git-Zweig>" # [required]&gt;&lt;img src="https://bluemix.net/deploy/button.png" alt="In Bluemix bereitstellen"&gt;&lt;/a&gt;
</pre>
</li>
<li>Markdown:
<p>
Standard-Master-Zweig:
</p>
<pre class="codeblock">
[&excl;[Deploy to Bluemix]&lpar;https://bluemix.net/deploy/button.png&rpar;]&lpar;https://bluemix.net/deploy?repository=&lt;git_repository_URL> # [required]&rpar;
</pre>
<p>Angegebener Git-Zweig:
</p>
<pre class="codeblock">
[&excl;[Deploy to Bluemix]&lpar;https://bluemix.net/deploy/button.png&rpar;]&lpar;https://bluemix.net/deploy?repository=&lt;git_repository_URL> &branch=&lt;git_branch&gt; # [required]&rpar;
</pre>
</li>
</ul>
</li>
<li>Fügen Sie das Snippet in Blogs, Artikel, Wikis, Readme-Dateien oder andere Dokumente ein, in denen Sie die App bekannt machen möchten. 
</li>
</ol>

##Aspekte zu Snippets für die Schaltfläche {: #button-snippet}

Ziehen Sie diese Aspekte bei der Anpassung des Snippets für Ihre Schaltfläche 'In Bluemix bereitstellen' zurate. 

* Beide Vorlagen verwenden einen Standardpfad zu einer externen Schaltflächengrafik im PNG-Format (in englischer Sprache). 

    * Wenn Sie anstelle des PNG-Formats eine SVG-Grafik für die Schaltfläche verwenden möchten, ist eine SVG-Version verfügbar. Sie können den Pfad zum im Snippet verwendeten externen Schaltflächenimage in `https://bluemix.net/deploy/button.svg` ändern.
	
	* Wenn Sie eine größere Grafik für die Schaltfläche verwenden möchten, gibt es eine im PNG-Format, die zweimal so groß wie das Original ist. Sie können den Pfad der im Snippet verwendeten externen Schaltflächengrafik in `https://bluemix.net/deploy/button_x2.png` ändern. 
	
	* Wenn Sie das Image lokal speichern möchten, können Sie es herunterladen und in Ihrem Git-Repository speichern. Passen Sie den Pfad so an, dass die relative Position der Grafik verwendet wird. 
	
	* Wenn Sie eine übersetzte Version der Schaltfläche verwenden möchten, können Sie sie über [ftp://public.dhe.ibm.com/cloud/bluemix/deploy_button![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](ftp://public.dhe.ibm.com/cloud/bluemix/deploy_button){:new_window} fern referenzieren oder von dort herunterladen. 
	
##Aspekte zu Repositorys für die Schaltfläche {: #button-repo} 

Ziehen Sie diese Aspekte für das Projektrepository zurate, das Sie für Ihre Schaltfläche 'In Bluemix bereitstellen' verwenden. 

<ul>
<li>Die Datei <code>manifest.yml</code> muss nicht im Repository vorhanden sein. Wenn für die Ausführung der App weitere Services erforderlich sind, müssen Sie jedoch eine Manifestdatei bereitstellen, die diese Services deklariert.  

Mit der Manifestdatei können Sie Folgendes angeben: 
    <ul>
    <li>Einen eindeutigen App-Namen.</li>  
    <li>Deklarierte Services: Eine Manifesterweiterung, die die erforderlichen oder optionalen Services erstellt (bzw. nach ihnen sucht), die eingerichtet werden müssen, bevor die App bereitgestellt wird (wie ein Datencache-Service). Sie können eine Liste der infrage kommenden {{site.data.keyword.Bluemix_notm}}-Services, -Bezeichnungen und -Pläne aufrufen, indem Sie die <a class="xref" href="https://github.com/cloudfoundry/cli/releases" target="_blank" title="(Wird in einer neuen Registerkarte oder in einem neuen Fenster geöffnet)">CF-Befehlszeilenschnittstelle <img class="image" src="../icons/launch-glyph.svg" alt="Symbol für externen Link"/></a> zum Ausführen des Befehls <code>cf marketplace</code> verwenden oder den <a class="xref" href="https://console.ng.bluemix.net/?ssoLogout=true&cm_mmc=developerWorks-_-dWdevcenter-_-devops-services-_-lp#/store" target="_blank" title="(Wird in einer neuen Registerkarte oder in einem neuen Fenster geöffnet)"> {{site.data.keyword.Bluemix_notm}}-Katalog<img class="image" src="../icons/launch-glyph.svg" alt="Symbol für externen Link"/></a> durchsuchen. 
    
        
    <strong>Hinweis:</strong> Deklarierte Services sind eine IBM Erweiterung des Cloud Foundry-Standardmanifestformats. Diese Erweiterung wird in einem zukünftigen Release möglicherweise im Rahmen der Weiterentwicklung und Verbesserung des Features überarbeitet.
	
	<a class="xref" href="http://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html#minimal-manifest" target="_blank" title="(Wird in einer neuen Registerkarte oder in einem neuen Fenster geöffnet)">Sie können sich informieren, wie eine Datei <code>manifest.yml</code> erstellt wird <img class="image" src="../icons/launch-glyph.svg" alt="Symbol für externen Link"/></a>.  
<pre class="codeblock">
	---
    #manifest.yml - Vorlage

  declared-services:
    &lt;`arbitrary_service_instance_name`&gt;:  # [erforderlich]
      label: &lt;`actual_service_name`&gt; # [erforderlich] Der tatsächliche Servicename aus dem Marktplatz
      plan: Shared # [optional] Dient zum Abrufen des deklarierten Service (falls angegeben). Andernfalls ist der Standardwert 'Free' oder 'free'.
  applications:
  - services
    - &lt;`arbitrary_service_instance_name`&gt;
    name: &lt;`appname`&gt;
    host: &lt;`apphostname`&gt;
</pre>

<pre class="codeblock">
	---
    #manifest.yml - Beispiel

  declared-services: 
      sample-java-cloudant-cloudantNoSQLDB: 
        label: cloudantNoSQLDB 
        plan: Shared 
  applications:
  - services
    - sample-java-cloudant-cloudantNoSQLDB
    name: My app
    host: myapp
</pre>
   </li>
   </ul>
	<li> Wenn die App vor der Bereitstellung zuerst erstellt werden muss, dann müssen Sie in Ihr Repository eine Builddatei einschließen. Wenn im Stammverzeichnis des Repositorys eine Build-Script-Datei gefunden wird, wird vor der Bereitstellung ein automatischer Build des Codes ausgelöst. 
	
	Unterstützte Buildprogramme: 
	    <ul>
		<li> <a class="xref" href="http://ant.apache.org/manual/using.html" target="_blank" title="(Wird in einer neuen Registerkarte oder in einem neuen Fenster geöffnet)">Ant:<img class="image" src="../icons/launch-glyph.svg" alt="Symbol für externen Link"/></a> /<code>build.xml</code>, mit Ausgabe an den Ordner <code>./output/</code> </li>
		<li> <a class="xref" href="http://docs.cloudfoundry.org/buildpacks/java/build-tool-int.html#gradle" target="_blank" title="(Wird in einer neuen Registerkarte oder in einem neuen Fenster geöffnet)">Gradle:<img class="image" src="../icons/launch-glyph.svg" alt="Symbol für externen Link"/></a> <code>/build.gradle</code>, mit Ausgabe an den Ordner <code>. </code> </li>
		<li> <a class="xref" href="http://gruntjs.com/getting-started#the-gruntfile" target="_blank" title="(Wird in einer neuen Registerkarte oder in einem neuen Fenster geöffnet)">Grunt:<img class="image" src="../icons/launch-glyph.svg" alt="Symbol für externen Link"/></a> <code>/Gruntfile.js</code>, mit Ausgabe an den Ordner <code>. </code> </li>
		<li> <a class="xref" href="http://docs.cloudfoundry.org/buildpacks/java/build-tool-int.html#maven" target="_blank" title="(Wird in einer neuen Registerkarte oder in einem neuen Fenster geöffnet)">Maven:<img class="image" src="../icons/launch-glyph.svg" alt="Symbol für externen Link"/></a> <code>/pom.xml</code>, mit Ausgabe an den Ordner <code>./target/</code></li>
	   </ul>
	</li>	
	<li>Zur Konfiguration einer Pipeline für das Projekt in einem Verzeichnis <code>.bluemix</code> fügen Sie eine Datei <code>pipeline.yml</code> ein. Sie können eine Datei mit der Bezeichnung <code>pipeline.yml</code> manuell erstellen oder sie auf der Grundlage eines vorhandenen DevOps Services-Projekts generieren. Führen Sie für die Erstellung einer Datei 'pipeline.yml' aus einem {{site.data.keyword.jazzhub_short}}-Projekt und zum Hinzufügen dieser Datei zu Ihrem Repository die folgenden Schritte aus. 
<ol>
<li>Öffnen Sie Ihr DevOps Services-Projekt in einem Browser und klicken Sie auf die Option zum Erstellen und Bereitstellen.</li>
<li>Konfigurieren Sie Ihre Pipeline mit Erstellungs- und Bereitstellungsjobs.</li>
<li>Fügen Sie in Ihrem Browser <code>/yaml</code> zur Projektpipeline-URL hinzu und drücken Sie die Eingabetaste. 
<br>Beispiel: <code>https://hub.jazz.net/pipeline/<Eigner>/<Projektname>/yaml</code></li>
<li>Speichern Sie die resultierende Datei <code>pipeline.yml</code>.</li>
<li>Erstellen Sie im Stammverzeichnis Ihres Projekts ein Verzeichnis <code>.bluemix</code>.</li>
<li>Laden Sie die Datei <code>pipeline.yml</code> in das Repository <code>.bluemix</code> hoch.</li>
</ol> </li>
	<li>Wenn Sie mithilfe von <strong>IBM Containers</strong> eine App in einem Container bereitstellen wollen, müssen Sie ins Stammverzeichnis des Repositorys eine Dockerfile und in ein Verzeichnis <code>.bluemix</code> eine Datei <code>pipeline.yml</code> aufnehmen. 
	<ul>
	    <li>Die Dockerfile fungiert als Build-Script für die App. Wenn eine Dockerfile im Repository festgestellt wird, dann wird die App automatisch in einem Image erstellt, bevor sie in einem Container bereitgestellt wird. Wenn die App selbst erstellt werden muss, bevor sie in einem Image erstellt wird, dann schließen Sie ein Build-Script für die App und auch eine Dockerfile (siehe vorherige Beschreibung) ein.</li>
	    <li> Weitere Informationen zur Erstellung von Dockerfiles finden Sie in der <a class="xref" href="https://docs.docker.com/reference/builder/" target="_blank" title="(Wird in einer neuen Registerkarte oder in einem neuen Fenster geöffnet)">Docker-Dokumentation <img class="image" src="../icons/launch-glyph.svg" alt="Symbol für externen Link"/></a>. </li>
	    <li>Sie können eine Datei mit der Bezeichnung <code>pipeline.yml</code> manuell erstellen oder sie auf der Grundlage eines vorhandenen DevOps Services-Projekts generieren. Informationen zum manuellen Erstellen einer Datei <code>pipeline.yml</code>, die speziell für Container vorgesehen ist, finden Sie in den <a class="xref" href="https://github.com/Puquios/" target="_blank" title="(Wird in einer neuen Registerkarte oder in einem neuen Fenster geöffnet)">Beispielen in GitHub <img class="image" src="../icons/launch-glyph.svg" alt="Symbol für externen Link"/></a>. </li>
        </ul>

 </li>
 </ul>
</ul>

Hilfe zur Fehlerbehebung finden Sie unter [Schaltfläche für die Bereitstellung in Bluemix führt nicht zum Bereitstellen einer App](/docs/troubleshoot/index.html#deploytobluemixbuttondoesntdeployanapp){:new_window}.	
