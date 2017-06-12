---
title: "&lt;serviceMetadata&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
ms.assetid: 2b4c3b4c-31d4-4908-a9b7-5bb411c221f2
caps.latest.revision: 28
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 28
---
# &lt;serviceMetadata&gt;
Gibt die Veröffentlichung der Dienstmetadaten und der zugeordneten Informationen an.  
  
## Syntax  
  
```  
  
<serviceMetadata   
    externalMetadataLocation="String"  
    httpGetBinding=”String”  
    httpGetBindingConfiguration=”String”  
    httpGetEnabled="Boolean"   
    httpGetUrl="String"  
    httpsGetBinding=”String”  
    httpsGetBindingConfiguration=”String”  
    httpsGetEnabled="Boolean"   
    httpsGetUrl="String"  
    policyVersion="Policy12/Policy15"/>  
```  
  
## Attribute und Elemente  
 In den folgenden Abschnitten werden Attribute sowie untergeordnete und übergeordnete Elemente beschrieben.  
  
### Attribute  
  
|Attribut|Beschreibung|  
|--------------|------------------|  
|externalMetadataLocation|Ein URI, der den Speicherort einer WSDL\-Datei enthält, die dem Benutzer als Antwort auf WSDL\- und MEX\-Anforderungen statt der automatisch generierten WSDL\-Datei zurückgegeben wird.  Wenn dieses Attribut nicht festgelegt wird, wird die WSDL\-Standarddatei zurückgegeben.  Der Standardwert ist eine leere Zeichenfolge.|  
|httpGetBinding|Eine Zeichenfolge, die den Typ der Bindung angibt, die für den Abruf von Metadaten mit HTTP GET verwendet wird.  Diese Einstellung ist optional.  Wenn nicht angegeben, werden die Standardbindungen verwendet.<br /><br /> Nur Bindungen mit inneren Bindungselementen, die <xref:System.ServiceModel.Channels.IReplyChannel> unterstützen, werden unterstützt.  Darüber hinaus muss die <xref:System.ServiceModel.Channels.MessageVersion%2A>\-Eigenschaft der Bindung <xref:System.ServiceModel.Channels.MessageVersion.None%2A> lauten.|  
|httpGetBindingConfiguration|Eine Zeichenfolge mit dem Namen der Bindung, die im `httpGetBinding`\-Attribut angegeben ist, das auf die zusätzlichen Konfigurationsinformationen dieser Bindung verweist.  Der gleiche Name muss im Abschnitt `<bindings>` definiert werden.|  
|httpGetEnabled|Ein boolescher Wert, der angibt, ob die Dienstmetadaten zum Abrufen anhand einer HTTP\/Get\-Anforderung veröffentlicht werden sollen.  Die Standardeinstellung ist `false`.<br /><br /> Falls das httpGetUrl\-Attribut nicht angegeben ist, ist die Adresse, an der die Metadaten veröffentlicht werden, die Dienstadresse plus ein "?wsdl".  Wenn die Dienstadresse beispielsweise "http:\/\/localhost:8080\/CalculatorService" lautet, ist die HTTP\/GET\-Metadatenadresse "http:\/\/localhost:8080\/CalculatorService? wsdl".<br /><br /> Falls diese Eigenschaft `false` lautet oder die Adresse des Diensts nicht auf HTTP oder HTTPS basiert, wird "?wsdl" ignoriert.|  
|httpGetUrl|Ein URI, der die Adresse angibt, an der die Metadaten zum Abrufen anhand einer HTTP\/Get\-Anforderung veröffentlicht werden.  Wenn ein relativer URI angegeben ist, wird er als relativ zur Basisadresse des Diensts behandelt.|  
|httpsGetBinding|Eine Zeichenfolge, die den Typ der Bindung angibt, die für den Abruf von Metadaten mit HTTPS GET verwendet wird.  Diese Einstellung ist optional.  Wenn nicht angegeben, werden die Standardbindungen verwendet.<br /><br /> Nur Bindungen mit inneren Bindungselementen, die <xref:System.ServiceModel.Channels.IReplyChannel> unterstützen, werden unterstützt.  Darüber hinaus muss die <xref:System.ServiceModel.Channels.MessageVersion%2A>\-Eigenschaft der Bindung <xref:System.ServiceModel.Channels.MessageVersion.None%2A> lauten.|  
|httpsGetBindingConfiguration|Eine Zeichenfolge mit dem Namen der Bindung, die im `httpsGetBinding`\-Attribut angegeben ist, das auf die zusätzlichen Konfigurationsinformationen dieser Bindung verweist.  Der gleiche Name muss im Abschnitt `<bindings>` definiert werden.|  
|httpsGetEnabled|Ein boolescher Wert, der angibt, ob die Dienstmetadaten zum Abrufen anhand einer HTTPS\/Get\-Anforderung veröffentlicht werden sollen.  Die Standardeinstellung ist `false`.<br /><br /> Falls das httpsGetUrl\-Attribut nicht angegeben ist, ist die Adresse, an der die Metadaten veröffentlicht werden, die Dienstadresse plus ein "?wsdl".  Wenn die Dienstadresse beispielsweise "https:\/\/localhost:8080\/CalculatorService" lautet, ist die HTTP\/GET\-Metadatenadresse "https:\/\/localhost:8080\/CalculatorService? wsdl".<br /><br /> Falls diese Eigenschaft `false` lautet oder die Adresse des Diensts nicht auf HTTP oder HTTPS basiert, wird "?wsdl" ignoriert.|  
|httpsGetUrl|Ein URI, der die Adresse angibt, an der die Metadaten zum Abrufen anhand einer HTTPS\/Get\-Anforderung veröffentlicht werden.|  
|policyVersion|Eine Zeichenfolge, die angibt, welche Version der WS\-Policy\-Spezifikation verwendet wird.  Dieses Attribut ist vom Typ <xref:System.ServiceModel.Description.PolicyVersion>.|  
  
### Untergeordnete Elemente  
 Keine  
  
### Übergeordnete Elemente  
  
|Element|Beschreibung|  
|-------------|------------------|  
|[\<Verhalten\>](../../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md)|Gibt ein Verhaltenselement an.|  
  
## Hinweise  
 Mit diesem Konfigurationselement können Sie die Metadatenveröffentlichungs\-Features eines Diensts steuern.  Um ein unbeabsichtigtes Veröffentlichen von möglicherweise vertraulichen Dienstmetadaten zu vermeiden, wird mit der Standardkonfiguration für [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)]\-Dienste die Metadatenveröffentlichung deaktiviert.  Dieses Verhalten ist in der Standardeinstellung sicher, bedeutet aber auch, dass man den zum Aufrufen des Diensts erforderlichen Clientcode nicht mithilfe eines Tools zum Importieren von Metadaten \(wie Svcutil.exe\) generieren kann. Dies ist nur dann möglich, wenn das Verhalten des Diensts zum Veröffentlichen von Metadaten in der Konfiguration explizit aktiviert ist.  Wenn Sie dieses Konfigurationselement verwenden, können Sie dieses Veröffentlichungsverhalten für Ihren Dienst aktivieren.  
  
 Ein ausführliches Codebeispiel für die Konfiguration dieses Verhaltens finden Sie unter [Metadatenveröffentlichungsverhalten](../../../../../docs/framework/wcf/samples/metadata-publishing-behavior.md).  
  
 Das optionale `httpGetBinding`\-Attribut und `httpsGetBinding`\-Attribut ermöglichen Ihnen das Konfigurieren der zum Abrufen der Metadaten über HTTP\-GET \(oder HTTPS\-GET\) verwendeten Bindungen.  Wenn sie nicht festgelegt sind, werden die Standardbindungen \(`HttpTransportBindingElement` für HTTP und `HttpsTransportBindingElement` für HTTPS\) entsprechend zum Abrufen der Metadaten verwendet.  Beachten Sie, dass Sie diese Attribute nicht mit den integrierten WCF\-Bindungen verwenden können.  Nur Bindungen mit inneren Bindungselementen, die <xref:System.ServiceModel.Channels.IReplyChannel> unterstützen, werden unterstützt.  Darüber hinaus muss die <xref:System.ServiceModel.Channels.MessageVersion%2A>\-Eigenschaft der Bindung <xref:System.ServiceModel.Channels.MessageVersion.None%2A> lauten.  
  
 Damit der Dienst möglichst gut vor böswilligen Benutzern geschützt wird, können Sie für die Übertragung den HTTPS\-Mechanismus \(SSL über HTTP\) verwenden.  Hierfür müssen Sie zunächst ein geeignetes X.509\-Zertifikat an einen bestimmten Port des Computers, auf dem der Dienst gehostet wird, binden.  \([!INCLUDE[crdefault](../../../../../includes/crdefault-md.md)] [Verwenden von Zertifikaten](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md).\) Fügen Sie dann dieses Element zur Dienstkonfiguration hinzu, und legen Sie für das `httpsGetEnabled`\-Attribut den Wert `true` fest.  Setzen Sie abschließend wie im folgenden Beispiel gezeigt das `httpsGetUrl`\-Attribut auf den URL des Dienstmetadaten\-Endpunkts:  
  
```  
<behaviors>  
 <serviceBehaviors>  
  <behavior name="NewBehavior">  
    <serviceMetadata httpsGetEnabled="true"   
     httpsGetUrl="https://myComputerName/myEndpoint" />  
  </behavior>  
 </serviceBehaviors>  
</behaviors>  
```  
  
## Beispiel  
 Im folgenden Beispiel wird ein Dienst anhand des \<serviceMetadata\>\-Elements konfiguriert, mit dem Metadaten verfügbar gemacht werden.  Es wird auch ein Endpunkt konfiguriert, mit dem der `IMetadataExchange`\-Vertrag als Implementierung eines WS\-MetadataExchange \(MEX\)\-Protokolls verfügbar gemacht wird.  In dem Beispiel wird `mexHttpBinding` verwendet, eine benutzerfreundliche Standardbindung, die `wsHttpBinding` entspricht und für die der Sicherheitsmodus auf `None` festgelegt ist.  Im Endpunkt wird eine relative Adresse von "mex" verwendet, die beim Auflösen der Dienstbasisadresse in einer Endpunktadresse von http:\/\/localhost\/servicemodelsamples\/service.svc\/mex resultiert.  
  
```  
<configuration>  
<system.serviceModel>  
  <services>  
    <service   
        name="Microsoft.ServiceModel.Samples.CalculatorService"  
        behaviorConfiguration="CalculatorServiceBehavior">  
      <!-- This endpoint is exposed at the base address provided by the host: http://localhost/servicemodelsamples/service.svc  -->  
      <endpoint address=""  
                binding="wsHttpBinding"  
                contract="Microsoft.ServiceModel.Samples.ICalculator" />  
      <!-- the mex endpoint is exposed at http://localhost/servicemodelsamples/service.svc/mex   
           To expose the IMetadataExchange contract, you   
           must enable the serviceMetadata behavior as demonstrated below -->  
      <endpoint address="mex"  
                binding="mexHttpBinding"  
                contract="IMetadataExchange" />  
    </service>  
  </services>  
  
  <!--For debugging purposes set the includeExceptionDetailInFaults attribute to true-->  
  <behaviors>  
    <serviceBehaviors>  
      <behavior name="CalculatorServiceBehavior">  
        <!-- The serviceMetadata behavior publishes metadata through   
             the IMetadataExchange contract. When this behavior is   
             present, you can expose this contract through an endpoint   
             as shown above. Setting httpGetEnabled to true publishes   
             the service's WSDL at the <baseaddress>?wsdl  
             eg. http://localhost/servicemodelsamples/service.svc?wsdl -->  
        <serviceMetadata httpGetEnabled="True"/>  
        <serviceDebug includeExceptionDetailInFaults="False" />  
      </behavior>  
    </serviceBehaviors>  
  </behaviors>  
  
</system.serviceModel>  
  
</configuration>  
```  
  
## Siehe auch  
 <xref:System.ServiceModel.Configuration.ServiceMetadataPublishingElement>   
 <xref:System.ServiceModel.Description.ServiceMetadataBehavior>   
 [Sicherheitsverhalten](../../../../../docs/framework/wcf/feature-details/security-behaviors-in-wcf.md)   
 [Metadatenveröffentlichungsverhalten](../../../../../docs/framework/wcf/samples/metadata-publishing-behavior.md)