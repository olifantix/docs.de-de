---
title: "Erweiterbarkeit des Workflowdiensthosts | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c0e8f7bb-cb13-49ec-852f-b85d7c23972f
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# Erweiterbarkeit des Workflowdiensthosts
[!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] stellt die <xref:System.ServiceModel.Activities.WorkflowServiceHost>\-Klasse zum Hosten von Workflowdiensten bereit.  Diese Klasse wird verwendet, wenn Sie einen Workflowdienst in einer verwalteten Anwendung oder einem Windows\-Dienst selbst hosten.  Diese Klasse wird auch verwendet, wenn Sie einen Workflow unter Internetinformationsdienste \(IIS\) oder dem Windows\-Prozessaktivierungsdienst \(WAS\) hosten.  Die <xref:System.ServiceModel.Activities.WorkflowServiceHost>\-Klasse stellt Erweiterungspunkte bereit, mit denen Sie benutzerdefinierte Erweiterungen hinzufügen, das Leerlaufverhalten ändern und andere Workflows als Dienstworkflows \(die keine Messagingaktivitäten nutzen\) hosten können.  
  
## Erweiterungen des Workflowdiensthosts  
 <xref:System.ServiceModel.Activities.WorkflowServiceHost> enthält eine <xref:System.ServiceModel.Activities.WorkflowServiceHost.WorkflowExtensions%2A>\-Eigenschaft vom Typ <xref:System.Activities.Hosting.WorkflowInstanceExtensionManager>, der Methoden zum Hinzufügen von Erweiterungen zu <xref:System.ServiceModel.Activities.WorkflowServiceHost> bereitstellt.  Verwenden Sie die <xref:System.Activities.Hosting.WorkflowInstanceExtensionManager.Add%2A>\-Methode zum Hinzufügen einer Erweiterung für jede Workflowdienstinstanz.  Der angegebene Delegat wird aufgerufen, um eine neue Erweiterung zu erstellen, wenn eine Workflowdienstinstanz erstellt oder aus einem Persistenzspeicher geladen wird.  Verwenden Sie die <xref:System.Activities.Hosting.WorkflowInstanceExtensionManager.Add%2A>\-Methode, um eine Erweiterung für jeden Workflowdiensthost hinzuzufügen. Eine Instanz der Erweiterung wird für alle Workflowdienstinstanzen genutzt.  
  
## Reagieren auf unbehandelte Ausnahmen  
 Das Verhalten <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior> ermöglicht das Angeben der Aktion, die ausgeführt werden soll, wenn innerhalb eines Workflowdiensts eine nicht behandelte Ausnahme auftritt.  Die <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior.Action%2A>\-Eigenschaft gibt einen der <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionAction>\-Werte an.  
  
-   <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionAction> – Bricht die Workflowdienstinstanz ab.  
  
-   <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionAction> – Führt einen Rollback zum letzten beibehaltenen Zustand aus, und unterbricht die Ausführung der Workflowdienstinstanz.  Dies ist nur der Fall, wenn der Workflow bereits mindestens einmal beibehalten wurde.  Falls nicht, wird die Workflowinstanz abgebrochen.  
  
-   <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionAction> – Bricht die Instanz ab.  
  
-   <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionAction> – Beendet die Instanz.  
  
 Dieses Verhalten kann im Code konfiguriert werden, wie im folgenden Beispiel gezeigt.  
  
```csharp  
host.Description.Behaviors.Add(new WorkflowUnhandledExceptionBehavior { Action = WorkflowUnhandledExceptionAction.Abandon });  
  
```  
  
 Es kann jedoch auch in einer Konfigurationsdatei konfiguriert werden, wie im folgenden Beispiel gezeigt.  
  
```vb-c#  
<behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <serviceMetadata httpGetEnabled="True"/>  
          <serviceDebug includeExceptionDetailInFaults="False" />  
          <workflowUnhandledExceptionBehavior action="Abandon" />        
        </behavior>  
      </serviceBehaviors>  
  
```  
  
## Hosten von anderen Workflows als Dienstworkflows  
 Mithilfe von <xref:System.ServiceModel.Activities.WorkflowServiceHost> können andere Workflows als Dienstworkflows gehostet werden. Außerdem können Workflows gehostet werden, die entweder nicht mit einer <xref:System.ServiceModel.Activities.Receive>\-Aktivität beginnen oder die keine Messagingaktivitäten verwenden.  Workflowdienste beginnen normalerweise mit einer <xref:System.ServiceModel.Activities.Receive>\-Aktivität.  Wenn der <xref:System.ServiceModel.Activities.WorkflowServiceHost> eine Nachricht für einen Workflowdienst empfängt, wird eine neue Workflowdienstinstanz erstellt, falls diese nicht bereits ausgeführt wird \(oder beibehalten wurde\).  Falls ein Workflow nicht mit einer Empfangsaktivität beginnt, kann er nicht mit dem Senden einer Nachricht gestartet werden, da keine Aktivität zum Empfangen der Nachricht vorhanden ist.  Um einen anderen Workflow als einen Dienstworkflow zu hosten, leiten Sie eine Klasse von <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint> ab und überschreiben <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint.OnGetInstanceId%2A>, <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint.OnGetCreationContext%2A> und <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint.OnResolveBookmark%2A>.  Überschreiben Sie <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint.OnGetInstanceId%2A>, wenn Sie eine bevorzugte Instanz\-ID bereitstellen möchten.  Überschreiben Sie <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint.OnGetCreationContext%2A>, um einen benutzerdefinierten Workflowerstellungskontext zu erstellen oder eine Instanz des vorhandenen <xref:System.ServiceModel.Activities.WorkflowCreationContext>\-Objekts aufzufüllen.  Überschreiben Sie <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint.OnResolveBookmark%2A>, um das Lesezeichen manuell aus der eingehenden Nachricht zu extrahieren.  Wenn Sie diese Methode überschreiben, müssen Sie in ihrem Text <xref:System.ServiceModel.Activities.WorkflowHostingResponseContext.SendResponse%2A> aufrufen, um auf die an den WorkflowHostingEndpoint gesendete Nachricht zu antworten.  Andernfalls wird möglicherweise der <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentCalls%2A>\-Grenzwert schließlich überschritten.  In bidirektionalen Verträgen können Sie eventuell feststellen, dass der Aufruf von <xref:System.ServiceModel.Activities.WorkflowHostingResponseContext.SendResponse%2A> fehlschlägt, weil der Client keine Antwort empfangen kann.  Bei unidirektionalen Verträgen erkennen Sie eventuell erst, wenn es zu spät ist, d. h. nachdem die <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentCalls%2A>\-Drosselungsgrenze überschritten wurde, dass <xref:System.ServiceModel.Activities.WorkflowHostingResponseContext.SendResponse%2A> nicht aufgerufen werden kann.  Weitere Informationen finden Sie im [WorkflowHostingEndpoint \- Lesezeichen\-Wiederaufnahme](../../../../docs/framework/windows-workflow-foundation/samples/workflowhostingendpoint-resume-bookmark.md)Um eine neue Instanz eines Nichtdienstworkflows zu erstellen, deklarieren Sie einen Dienstvertrag, der einen Vorgang zur Erstellung einer neuen Instanz definiert.  Für den Erstellungsvorgang sollte ein IDictionary\<string, object\> verwendet werden, um die erforderliche Workflowparameter zu übergeben.  Dieser Vertrag wird implizit von der Klasse implementiert, die von <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint> abgeleitet wurde.  Fügen Sie dem Host beim Hosten des Workflows eine Instanz der von <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint> abgeleiteten Klasse hinzu, indem Sie <xref:System.ServiceModel.Activities.WorkflowServiceHost.Open%2A> aufrufen, und rufen Sie dann <xref:System.ServiceModel.Activities.WorkflowServiceHost.AddServiceEndpoint%2A> auf.  Um eine Instanz des Workflows zu erstellen, erstellen Sie für Ihren Dienstvertrag ein <xref:System.ServiceModel.ChannelFactory%601>\-Objekt, und rufen Sie anschließend <xref:System.ServiceModel.ChannelFactory%601.CreateChannel%2A> auf.  Sie können dann den im Dienstvertrag definierten Erstellungsvorgang aufrufen.  
  
## Siehe auch  
 [Workflowdienste](../../../../docs/framework/wcf/feature-details/workflow-services.md)   
 [Messagingaktivitäten](../../../../docs/framework/wcf/feature-details/messaging-activities.md)