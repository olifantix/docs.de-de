---
title: "Initialisierung der Instanziierung | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 154d049f-2140-4696-b494-c7e53f6775ef
caps.latest.revision: 31
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 31
---
# Initialisierung der Instanziierung
In diesem Beispiel wird das [Pooling](../../../../docs/framework/wcf/samples/pooling.md)\-Beispiel erweitert, indem die Schnittstelle `IObjectControl` definiert wird, die die Initialisierung eines Objekts durch Aktivieren und Deaktivieren anpasst.Der Client ruft Methoden auf, die das Objekt an den Pool zurückgeben und das Objekt nicht an den Pool zurückgeben.  
  
> [!NOTE]
>  Die Setupprozedur und die Buildanweisungen für dieses Beispiel befinden sich am Ende dieses Themas.  
  
## Erweiterungspunkte  
 Der erste Schritt beim Erstellen einer [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]\-Erweiterung besteht darin, den zu verwendenden Erweiterungspunkt auszuwählen.In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] bezeichnet *EndpointDispatcher* eine Laufzeitkomponente, die eingehende Nachrichten in Methodenaufrufe für den Dienst des Benutzers konvertiert und Rückgabewerte von dieser Methode in eine ausgehende Nachricht konvertiert.Ein [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-Dienst erstellt einen EndpointDispatcher für jeden Endpunkt.  
  
 Der EndpointDispatcher stellt mithilfe der <xref:System.ServiceModel.Dispatcher.EndpointDispatcher>\-Klasse die Erweiterung des Endpunktbereichs bereit \(für alle vom Dienst empfangenen oder gesendeten Nachrichten\).Mit dieser Klasse können Sie verschiedene Eigenschaften anpassen, die das Verhalten von EndpointDispatcher steuern.In diesem Beispiel wird in erster Linie die <xref:System.ServiceModel.Dispatcher.DispatchRuntime.InstanceProvider%2A>\-Eigenschaft behandelt, die auf das Objekt zeigt, das die Instanzen der Dienstklasse bereitstellt.  
  
## IInstanceProvider  
 In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] erstellt EndpointDispatcher mithilfe eines Instanzenanbieters, der die <xref:System.ServiceModel.Dispatcher.IInstanceProvider>\-Schnittstelle implementiert, Instanzen einer Dienstklasse.Diese Schnittstelle verfügt über nur zwei Methoden:  
  
-   <xref:System.ServiceModel.Dispatcher.IInstanceProvider.GetInstance%2A>: Wenn eine Nachricht eingeht, ruft der Verteiler die <xref:System.ServiceModel.Dispatcher.IInstanceProvider.GetInstance%2A>\-Methode auf, um eine Instanz der Dienstklasse zum Verarbeiten der Nachricht zu erstellen.Die Häufigkeit der Aufrufe dieser Methode wird von der <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A>\-Eigenschaft bestimmt.Wenn die <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A>\-Eigenschaft beispielsweise auf <xref:System.ServiceModel.InstanceContextMode?displayProperty=fullName> festgelegt ist, wird eine neue Instanz der Dienstklasse erstellt, um alle eingehenden Nachrichten zu verarbeiten. Daher wird <xref:System.ServiceModel.Dispatcher.IInstanceProvider.GetInstance%2A> immer dann aufgerufen, wenn eine Nachricht eingeht.  
  
-   <xref:System.ServiceModel.Dispatcher.IInstanceProvider.ReleaseInstance%2A>: Wenn die Dienstinstanz das Verarbeiten der Nachricht abgeschlossen hat, ruft EndpointDispatcher die <xref:System.ServiceModel.Dispatcher.IInstanceProvider.ReleaseInstance%2A>\-Methode auf.Wie bei der <xref:System.ServiceModel.Dispatcher.IInstanceProvider.GetInstance%2A>\-Methode wird die Häufigkeit der Aufrufe dieser Methode von der <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A>\-Eigenschaft bestimmt.  
  
## Der Objektpool  
 Die `ObjectPoolInstanceProvider`\-Klasse enthält die Implementierung des Objektpools.Diese Klasse implementiert die <xref:System.ServiceModel.Dispatcher.IInstanceProvider>\-Schnittstelle für die Interaktion mit der Dienstmodellebene.Wenn EndpointDispatcher die <xref:System.ServiceModel.Dispatcher.IInstanceProvider.GetInstance%2A>\-Methode aufruft, erstellt die benutzerdefinierte Implementierung keine neue Instanz, sondern sucht ein vorhandenes Objekt in einem Pool im Speicher.Wenn ein Objekt verfügbar ist, wird es zurückgegeben.Andernfalls überprüft `ObjectPoolInstanceProvider`, ob die `ActiveObjectsCount`\-Eigenschaft \(Anzahl der aus dem Pool zurückgegebenen Objekte\) die maximale Poolgröße erreicht hat.Wenn dies nicht der Fall ist, wird eine neue Instanz erstellt und an den Aufrufer zurückgegeben, und anschließend wird `ActiveObjectsCount` inkrementiert.Andernfalls wird eine Objekterstellungsanforderung für einen konfigurierten Zeitraum in die Warteschlange gestellt.Die Implementierung für `GetObjectFromThePool` wird im folgenden Beispielcode dargestellt.  
  
```  
  
private object GetObjectFromThePool()  
{  
    bool didNotTimeout =   
       availableCount.WaitOne(creationTimeout, true);  
    if(didNotTimeout)  
    {  
         object obj = null;  
         lock (poolLock)  
        {  
             if (pool.Count != 0)  
             {  
                   obj = pool.Pop();  
                   activeObjectsCount++;  
             }  
             else if (pool.Count == 0)  
             {  
                   if (activeObjectsCount < maxPoolSize)  
                   {  
                        obj = CreateNewPoolObject();  
                        activeObjectsCount++;  
  
                        #if (DEBUG)  
                        WritePoolMessage(  
                             ResourceHelper.GetString("MsgNewObject"));  
                       #endif  
                   }                          
            }  
           idleTimer.Stop();  
      }  
     // Call the Activate method if possible.  
    if (obj is IObjectControl)  
   {  
         ((IObjectControl)obj).Activate();  
   }  
   return obj;  
}  
throw new TimeoutException(  
ResourceHelper.GetString("ExObjectCreationTimeout"));  
}  
```  
  
 Die benutzerdefinierte `ReleaseInstance`\-Implementierung fügt die freigegebene Instanz dem Pool erneut hinzu und dekrementiert den `ActiveObjectsCount`\-Wert.EndpointDispatcher kann diese Methoden von unterschiedlichen Threads aus aufrufen. Daher ist ein synchronisierter Zugriff auf die Member der Klassenebene in der `ObjectPoolInstanceProvider`\-Klasse erforderlich.  
  
```  
public void ReleaseInstance(InstanceContext instanceContext, object instance)  
{  
    lock (poolLock)  
    {  
        // Check whether the object can be pooled.   
        // Call the Deactivate method if possible.  
        if (instance is IObjectControl)  
        {  
            IObjectControl objectControl = (IObjectControl)instance;  
            objectControl.Deactivate();  
  
            if (objectControl.CanBePooled)  
            {  
                pool.Push(instance);  
  
                #if(DEBUG)  
                WritePoolMessage(  
                    ResourceHelper.GetString("MsgObjectPooled"));  
                #endif                          
            }  
            else  
            {  
                #if(DEBUG)  
                WritePoolMessage(  
                    ResourceHelper.GetString("MsgObjectWasNotPooled"));  
                #endif  
            }  
        }  
        else  
        {  
            pool.Push(instance);  
  
            #if(DEBUG)  
            WritePoolMessage(  
                ResourceHelper.GetString("MsgObjectPooled"));  
            #endif   
        }  
  
        activeObjectsCount--;  
  
        if (activeObjectsCount == 0)  
        {  
            idleTimer.Start();                       
        }  
    }  
  
    availableCount.Release(1);  
}  
  
```  
  
 Die `ReleaseInstance`\-Methode stellt ein Feature zur *Bereinigungsinitialisierung* bereit.Normalerweise wird im Pool eine Mindestanzahl von Objekten für die Lebensdauer des Pools beibehalten.Es kann jedoch Zeiten mit übermäßiger Auslastung geben, für die im Pool zusätzliche Objekte erstellt werden müssen, um die in der Konfiguration festgelegte Höchstgrenze zu erreichen.Wenn der Pool weniger aktiv ist, stellen diese überzähligen Objekte einen zusätzlichen Aufwand dar.Wenn `activeObjectsCount` daher 0 \(null\) erreicht, wird ein Leerlaufzeitgeber gestartet, der einen Bereinigungszyklus auslöst und ausführt.  
  
```  
if (activeObjectsCount == 0)  
{  
    idleTimer.Start();   
}  
  
```  
  
 ServiceModel\-Ebenenerweiterungen werden mithilfe der folgenden Verhalten verknüpft:  
  
-   Dienstverhalten: Diese ermöglichen die Anpassung der ganzen Dienstlaufzeit.  
  
-   Endpunktverhalten: Diese ermöglichen das Anpassen eines bestimmten Dienstendpunkts, einschließlich EndpointDispatcher.  
  
-   Vertragsverhalten: Diese ermöglichen das Anpassen von <xref:System.ServiceModel.Dispatcher.ClientRuntime>\-Klassen oder <xref:System.ServiceModel.Dispatcher.DispatchRuntime>\-Klassen auf dem Client bzw. Server.  
  
-   Vorgangsverhalten: Diese ermöglichen das Anpassen von <xref:System.ServiceModel.Dispatcher.ClientOperation>\-Klassen oder <xref:System.ServiceModel.Dispatcher.DispatchOperation>\-Klassen auf dem Client bzw. Server.  
  
 Für den Zweck einer Objektpoolingerweiterung kann ein Endpunktverhalten oder ein Dienstverhalten erstellt werden.In diesem Beispiel wird ein Dienstverhalten verwendet, das die Objektpoolingfähigkeit auf alle Endpunkte des Diensts anwendet.Dienstverhaltensweisen werden durch Implementieren der <xref:System.ServiceModel.Description.IServiceBehavior>\-Schnittstelle erstellt.Es gibt mehrere Möglichkeiten, ServiceModel auf die benutzerdefinierten Verhaltensweisen hinzuweisen:  
  
-   Verwenden eines benutzerdefinierten Attributs.  
  
-   Imperatives Hinzufügen zur Verhaltensauflistung der Dienstbeschreibung.  
  
-   Erweitern der Konfigurationsdatei.  
  
 In diesem Beispiel wird ein benutzerdefiniertes Attribut verwendet.Beim Erstellen von <xref:System.ServiceModel.ServiceHost> werden die in der Typdefinition des Diensts verwendeten Attribute untersucht, und die verfügbaren Verhalten werden der Verhaltensauflistung der Dienstbeschreibung hinzugefügt.  
  
 Die <xref:System.ServiceModel.Description.IServiceBehavior>\-Schnittstelle verfügt über drei Methoden: <xref:System.ServiceModel.Description.IServiceBehavior.Validate%2A>`,` <xref:System.ServiceModel.Description.IServiceBehavior.AddBindingParameters%2A>`,` und <xref:System.ServiceModel.Description.IServiceBehavior.ApplyDispatchBehavior%2A>.Diese Methoden werden von [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] aufgerufen, wenn <xref:System.ServiceModel.ServiceHost> initialisiert wird.<xref:System.ServiceModel.Description.IServiceBehavior.Validate%2A?displayProperty=fullName> wird zuerst aufgerufen. So kann der Dienst auf Inkonsistenzen untersucht werden.<xref:System.ServiceModel.Description.IServiceBehavior.AddBindingParameters%2A?displayProperty=fullName> wird danach aufgerufen. Diese Methode ist nur in sehr komplexen Szenarios erforderlich.<xref:System.ServiceModel.Description.IServiceBehavior.ApplyDispatchBehavior%2A?displayProperty=fullName> wird zuletzt aufgerufen und ist für das Konfigurieren der Laufzeit zuständig.Die folgenden Parameter werden in <xref:System.ServiceModel.Description.IServiceBehavior.ApplyDispatchBehavior%2A?displayProperty=fullName> übergeben:  
  
-   `Description`: Dieser Parameter stellt die Dienstbeschreibung für den gesamten Dienst bereit.Dies kann verwendet werden, um Beschreibungsdaten über die Endpunkte, Verträge, Bindungen und andere Daten zu dem Dienst zu überprüfen.  
  
-   `ServiceHostBase`: Dieser Parameter stellt die <xref:System.ServiceModel.ServiceHostBase> bereit, die gerade initialisiert wird.  
  
 In der benutzerdefinierten <xref:System.ServiceModel.Description.IServiceBehavior>\-Implementierung wird eine neue Instanz von `ObjectPoolInstanceProvider` instanziiert und der <xref:System.ServiceModel.Dispatcher.DispatchRuntime.InstanceProvider%2A>\-Eigenschaft in jedem <xref:System.ServiceModel.Dispatcher.EndpointDispatcher> zugewiesen, der <xref:System.ServiceModel.ServiceHostBase> angefügt ist.  
  
```  
public void ApplyDispatchBehavior(ServiceDescription description, ServiceHostBase serviceHostBase)  
{  
    if (enabled)  
    {  
        // Create an instance of the ObjectPoolInstanceProvider.  
        instanceProvider = new ObjectPoolInstanceProvider(description.ServiceType,  
        maxPoolSize, minPoolSize, creationTimeout);  
  
        // Assign our instance provider to Dispatch behavior in each   
        // endpoint.  
        foreach (ChannelDispatcherBase cdb in serviceHostBase.ChannelDispatchers)  
        {  
             ChannelDispatcher cd = cdb as ChannelDispatcher;  
             if (cd != null)  
             {  
                 foreach (EndpointDispatcher ed in cd.Endpoints)  
                 {  
                        ed.DispatchRuntime.InstanceProvider = instanceProvider;  
                 }  
             }  
         }  
     }  
}   
```  
  
 Neben einer <xref:System.ServiceModel.Description.IServiceBehavior>\-Implementierung verfügt die `ObjectPoolingAttribute`\-Klasse über mehrere Member zum Anpassen des Objektpools mithilfe der Attributargumente.Diese Member umfassen `MaxSize`, `MinSize`, `Enabled` und `CreationTimeout` für die Übereinstimmung mit dem von .NET Enterprise Services bereitgestellten Objektpooling\-Featuresatz.  
  
 Das Objektpoolingverhalten kann nun einem [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-Dienst hinzugefügt werden, indem der Dienstimplementierung mit dem neu erstellten, benutzerdefinierten `ObjectPooling`\-Attribut eine Anmerkung hinzugefügt wird.  
  
```  
[ObjectPooling(MaxSize=1024, MinSize=10, CreationTimeout=30000]      
public class PoolService : IPoolService  
{  
  // …  
}  
```  
  
## Aktivieren und Deaktivieren von Verknüpfungen  
 Das primäre Ziel des Objektpoolings ist das Optimieren von Objekten mit kurzer Lebensdauer und relativ aufwändiger Erstellung und Initialisierung.Bei der richtigen Verwendung kann daher eine erhebliche Leistungssteigerung erreicht werden.Da das Objekt aus dem Pool zurückgegeben wird, wird der Konstruktor nur einmal aufgerufen.Bei einigen Anwendungen ist jedoch eine gewisse Kontrolle erforderlich, damit sie die in einem einzigen Kontext verwendeten Ressourcen initialisieren und bereinigen können.Ein Objekt, das beispielsweise für eine Gruppe von Berechnungen verwendet wird, kann die privaten Felder zurücksetzen, bevor die nächste Berechnung verarbeitet wird.In Enterprise Services wurde diese Art der kontextspezifischen Initialisierung ermöglicht, indem der Objektentwickler die `Activate`\-Methode und die `Deactivate`\-Methode in der <xref:System.EnterpriseServices.ServicedComponent>\-Basisklasse überschreiben konnte.  
  
 Der Objektpool ruft die `Activate`\-Methode unmittelbar vor dem Zurückgeben des Objekts aus dem Pool auf.`Deactivate` wird aufgerufen, wenn das Objekt an den Pool zurückgegeben wird.Die <xref:System.EnterpriseServices.ServicedComponent>\-Basisklasse verfügt außerdem über die `boolean`\-Eigenschaft mit der Bezeichnung `CanBePooled`, mit der der Pool darüber benachrichtigt werden kann, ob das Objekt weiter gepoolt werden kann.  
  
 Im Beispiel wird eine öffentliche Schnittstelle \(`IObjectControl`\) deklariert, die über die oben genannten Member verfügt, um diese Funktionalität zu imitieren.Diese Schnittstelle wird dann von Dienstklassen implementiert, die die kontextspezifische Initialisierung bereitstellen sollen.Die <xref:System.ServiceModel.Dispatcher.IInstanceProvider>\-Implementierung muss geändert werden, um diese Anforderungen zu erfüllen.Wenn Sie nun ein Objekt durch Aufrufen der `GetInstance`\-Methode abrufen, müssen Sie jedes Mal überprüfen, ob das Objekt `IObjectControl.`  implementiert. Wenn dies der Fall ist, müssen Sie die `Activate`\-Methode entsprechend aufrufen.  
  
```  
if (obj is IObjectControl)  
{  
    ((IObjectControl)obj).Activate();  
}  
  
```  
  
 Beim Zurückgeben eines Objekts an den Pool ist eine Überprüfung für die `CanBePooled`\-Eigenschaft erforderlich, bevor das Objekt erneut dem Pool hinzugefügt wird.  
  
```  
if (instance is IObjectControl)  
{  
    IObjectControl objectControl = (IObjectControl)instance;  
    objectControl.Deactivate();  
    if (objectControl.CanBePooled)  
    {  
       pool.Push(instance);  
    }  
}  
  
```  
  
 Da der Dienstentwickler entscheiden kann, ob ein Objekt gepoolt werden kann, kann die Objektanzahl im Pool zu einem bestimmten Zeitpunkt unter dem Mindestwert liegen.Sie müssen daher überprüfen, ob die Objektanzahl unter dem Mindestwert liegt, und die erforderliche Initialisierung in der Bereinigungsprozedur ausführen.  
  
```  
// Remove the surplus objects.  
if (pool.Count > minPoolSize)  
{  
  // Clean the surplus objects.  
}                      
else if (pool.Count < minPoolSize)  
{  
  // Reinitialize the missing objects.  
  while(pool.Count != minPoolSize)  
  {  
    pool.Push(CreateNewPoolObject());  
  }  
}  
```  
  
 Wenn Sie das Beispiel ausführen, werden die Anforderungen und Antworten für den Vorgang im Dienst\- und Clientkonsolenfenster angezeigt.Drücken Sie die EINGABETASTE in den einzelnen Konsolenfenstern, um den Dienst und den Client zu schließen.  
  
#### So richten Sie das Beispiel ein, erstellen es und führen es aus  
  
1.  Stellen Sie sicher, dass Sie [Einmaliges Setupverfahren für Windows Communication Foundation\-Beispiele](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md) ausgeführt haben.  
  
2.  Folgen Sie zum Erstellen der Projektmappe den unter [Erstellen der Windows Communication Foundation\-Beispiele](../../../../docs/framework/wcf/samples/building-the-samples.md) aufgeführten Anweisungen.  
  
3.  Wenn Sie das Beispiel in einer Konfiguration mit einem Computer oder über Computer hinweg ausführen möchten, folgen Sie den unter [Durchführen der Windows Communication Foundation\-Beispiele](../../../../docs/framework/wcf/samples/running-the-samples.md) aufgeführten Anweisungen.  
  
> [!IMPORTANT]
>  Die Beispiele sind möglicherweise bereits auf dem Computer installiert.Suchen Sie nach dem folgenden Verzeichnis \(Standardverzeichnis\), bevor Sie fortfahren.  
>   
>  `<Installationslaufwerk>:\WF_WCF_Samples`  
>   
>  Wenn dieses Verzeichnis nicht vorhanden ist, rufen Sie [Windows Communication Foundation \(WCF\) and Windows Workflow Foundation \(WF\) Samples for .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) auf, um alle [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]\- und [!INCLUDE[wf1](../../../../includes/wf1-md.md)]\-Beispiele herunterzuladen.Dieses Beispiel befindet sich im folgenden Verzeichnis.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Instancing\Initialization`  
  
## Siehe auch