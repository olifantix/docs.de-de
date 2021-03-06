---
title: 'Vorgehensweise: Aktivieren der SQL-Persistenz für Workflows und Workflowdienste'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: ca7bf77f-3e5d-4b23-b17a-d0b60f46411d
ms.openlocfilehash: 6bcd47f3a750659651d099519d5e1f435be01ab2
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="how-to-enable-sql-persistence-for-workflows-and-workflow-services"></a>Vorgehensweise: Aktivieren der SQL-Persistenz für Workflows und Workflowdienste
In diesem Thema wird beschrieben, wie Sie die Funktion „SQL-Workflowinstanzspeicher“ konfigurieren, um die Persistenz für Workflows und Workflowdienste sowohl programmgesteuert als auch mithilfe einer Konfigurationsdatei zu aktivieren.  
  
 Windows Server AppFabric vereinfacht die Konfiguration von Persistenz. Weitere Informationen finden Sie unter [App Fabric Persistenz-Konfiguration](http://go.microsoft.com/fwlink/?LinkId=201204)  
  
 Erstellen Sie vor dem Verwenden der Funktion „SQL-Workflowinstanzspeicher“ eine Datenbank erstellen, die die Funktion zum Beibehalten von Workflowinstanzen verwendet. Das [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)]-Setupprogramm kopiert die SQL-Skriptdateien, die der Funktion "SQL-Workflowinstanzspeicher" zugeordnet sind, in den Ordner "%WINDIR%\Microsoft.NET\Framework\v4.xxx\SQL\EN". Führen Sie diese Skriptdateien für eine SQL Server 2005- oder SQL Server 2008-Datenbank aus, die der SQL-Workflowinstanzspeicher zum Beibehalten von Workflowinstanzen verwenden soll. Führen Sie zuerst die Datei "SqlWorkflowInstanceStoreSchema.sql" und dann die Datei "SqlWorkflowInstanceStoreLogic.sql" aus.  
  
> [!NOTE]
>  Um die Persistenzdatenbank so zu bereinigen, dass sie eine neue Datenbank aufweist, führen Sie die Skripts in "%WINDIR%\Microsoft.NET\Framework\v4.xxx\SQL\EN" in der folgenden Reihenfolge aus.  
>   
>  1.  SqlWorkflowInstanceStoreSchema.sql  
> 2.  SqlWorkflowInstanceStoreLogic.sql  
  
> [!IMPORTANT]
>  Wenn Sie keine Persistenzdatenbank erstellen, löst die Funktion "SQL-Workflowinstanzspeicher" eine Ausnahme wie unten angegeben aus, sobald ein Host versucht, Workflows beizubehalten.  
>   
>  System.Data.SqlClient.SqlException: Die gespeicherte Prozedur "System.Activities.DurableInstancing.CreateLockOwner" wurde nicht gefunden.  
  
 In den folgenden Abschnitten wird beschrieben, wie Sie die Persistenz für Workflows und Workflowdienste mithilfe des SQL-Workflowinstanzspeichers aktivieren. Weitere Informationen zu den Eigenschaften des SQL-Workflowinstanzspeichers finden Sie unter [Eigenschaften des SQL-Workflowinstanzspeicher](../../../docs/framework/windows-workflow-foundation/properties-of-sql-workflow-instance-store.md).  
  
## <a name="enabling-persistence-for-self-hosted-workflows-that-use-workflowapplication"></a>Aktivieren der Persistenz für selbst gehostete Workflows, die WorkflowApplication verwenden  
 Sie können die Persistenz für selbst gehostete Workflows aktivieren, die <xref:System.Activities.WorkflowApplication> programmgesteuert nutzen, indem Sie das <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore>-Objektmodell verwenden. Die folgende Vorgehensweise enthält die dafür erforderlichen Schritte.  
  
#### <a name="to-enable-persistence-for-self-hosted-workflows"></a>So aktivieren Sie Persistenz für selbst gehostete Workflows  
  
1.  Fügen Sie einen Verweis zu "System.Activites.DurableInstancing.dll" hinzu.  
  
2.  Fügen Sie oben in der Quelldatei nach den vorhandenen using-Anweisungen die folgende Anweisung hinzu.  
  
    ```csharp  
    using System.Activities.DurableInstancing;  
    ```  
  
3.  Erstellen Sie einen <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore>, und weisen Sie ihn dem<xref:System.Activities.WorkflowApplication.InstanceStore%2A> der <xref:System.Activities.WorkflowApplication> wie im folgenden Codebeispiel dargestellt zu.  
  
    ```csharp  
    SqlWorkflowInstanceStore store =   
        new SqlWorkflowInstanceStore("Server=.\\SQLEXPRESS;Initial Catalog=Persistence;Integrated Security=SSPI");  
  
    WorkflowApplication wfApp =  
        new WorkflowApplication(new Workflow1());  
  
    wfApp.InstanceStore = store;  
    ```  
  
    > [!NOTE]
    >  Abhängig von der SQL Server-Version kann der Servername der Verbindungszeichenfolge abweichen.  
  
4.  Rufen Sie die <xref:System.Activities.WorkflowApplication.Persist%2A>-Methode für das <xref:System.Activities.WorkflowApplication>-Objekt auf, um einen Workflow beizubehalten, oder die <xref:System.Activities.WorkflowApplication.Unload%2A>-Methode, um einen Workflow beizubehalten und zu entladen. Sie können auch das vom <xref:System.Activities.WorkflowApplication.PersistableIdle%2A>-Objekt ausgelöste <xref:System.Activities.WorkflowApplication>-Ereignis behandeln und den entsprechenden Member (<xref:System.Activities.PersistableIdleAction.Persist> oder <xref:System.Activities.PersistableIdleAction.Unload>) von <xref:System.Activities.PersistableIdleAction> zurückgeben.  
  
    ```csharp  
    wfApp.PersistableIdle = delegate(WorkflowApplicationIdleEventArgs e)  
    {  
        return PersistableIdleAction.Persist;  
    };  
    ```  
  
> [!NOTE]
>  Finden Sie unter der [beibehalten einer Workflowanwendung](../../../docs/framework/windows-workflow-foundation/samples/persisting-a-workflow-application.md) -Beispiel unter [Persistenz](../../../docs/framework/windows-workflow-foundation/samples/persistence.md) für ein Beispiel für das Aktivieren der Persistenz für Workflows mit der <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore>, und die [Vorgehensweise: Erstellen und Ausführen einer Long-Wert Workflow ausgeführt wird,](../../../docs/framework/windows-workflow-foundation/how-to-create-and-run-a-long-running-workflow.md) Schritt der [Lernprogramm für erste Schritte](../../../docs/framework/windows-workflow-foundation/getting-started-tutorial.md) Schritt-für-Schritt-Anweisungen.  
  
## <a name="enabling-persistence-for-self-hosted-workflow-services-that-use-the-workflowservicehost"></a>Aktivieren der Persistenz für selbst gehostete Workflowdienste, die WorkflowServiceHost verwenden  
 Sie können die Persistenz für selbst gehostete Workflowdienste, die <xref:System.ServiceModel.WorkflowServiceHost> verwenden, mithilfe der <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior>-Klasse oder der <xref:System.ServiceModel.Activities.WorkflowServiceHost.DurableInstancingOptions%2A>-Klasse programmgesteuert aktivieren.  
  
### <a name="using-the-sqlworkflowinstancestorebehavior-class"></a>Verwenden der SqlWorkflowInstanceStoreBehavior-Klasse  
 Die folgende Vorgehensweise enthält Schritte zum Verwenden der <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior>-Klasse zur Aktivierung der Persistenz für selbst gehostete Workflowdienste.  
  
##### <a name="to-enable-persistence-using-sqlworkflowinstancestorebehavior"></a>So aktivieren Sie die Persistenz mit SqlWorkflowInstanceStoreBehavior  
  
1.  Fügen Sie einen Verweis zu "System.ServiceModel.dll" hinzu.  
  
2.  Fügen Sie oben in der Quelldatei nach den vorhandenen using-Anweisungen die folgende Anweisung hinzu.  
  
    ```csharp  
    using System.ServiceModel.Activities.Description;  
    ```  
  
3.  Erstellen Sie eine Instanz von `WorkflowServiceHost`, und fügen Sie Endpunkte für den Workflowdienst hinzu.  
  
    ```  
    WorkflowServiceHost host = new WorkflowServiceHost(new CountingWorkflow(), new Uri(hostBaseAddress));  
    host.AddServiceEndpoint("ICountingWorkflow", new BasicHttpBinding(), "");  
    ```  
  
4.  Erstellen Sie ein `SqlWorkflowInstanceStoreBehavior`-Objekt, und legen Sie Eigenschaften des Verhaltensobjekts fest.  
  
    ```csharp  
    SqlWorkflowInstanceStoreBehavior instanceStoreBehavior = new SqlWorkflowInstanceStoreBehavior(connectionString);  
    instanceStoreBehavior.HostLockRenewalPeriod = new TimeSpan(0, 0, 5);  
    instanceStoreBehavior.InstanceCompletionAction = InstanceCompletionAction.DeleteAll;  
    instanceStoreBehavior.InstanceLockedExceptionAction = InstanceLockedExceptionAction.AggressiveRetry;  
    instanceStoreBehavior.InstanceEncodingOption = InstanceEncodingOption.GZip;  
    instanceStoreBehavior.RunnableInstancesDetectionPeriod = new TimeSpan("00:00:02");  
    host.Description.Behaviors.Add(instanceStoreBehavior);  
    ```  
  
5.  Öffnen Sie den Workflowdiensthost.  
  
    ```vb  
    host.Open();  
    ```  
  
> [!IMPORTANT]
>  Finden Sie unter der [integrierte](../../../docs/framework/windows-workflow-foundation/samples/built-in-configuration.md) -Beispiel unter [Persistenz](../../../docs/framework/windows-workflow-foundation/samples/persistence.md) für ein Beispiel für das Aktivieren der Persistenz für Workflowdienste mithilfe der `SqlWorkflowInstanceStoreBehavior` Klasse.  
  
### <a name="using-the-durableinstancingoptions-property"></a>Verwenden der DurableInstancingOptions-Eigenschaft  
 Wenn `SqlWorkflowInstanceStoreBehavior` angewendet wird, wird `DurableInstancingOptions.InstanceStore` auf dem `WorkflowServiceHost` auf das `SqlWorkflowInstanceStore`-Element festgelegt, das anhand der Konfigurationswerte erstellt wurde. Dies können Sie auch programmgesteuert erreichen, um die <xref:System.ServiceModel.Activities.WorkflowServiceHost.DurableInstancingOptions%2A>-Eigenschaft von `WorkflowServiceHost` ohne Verwendung der `SqlWorkflowInstanceStoreBehavior`-Klasse festzulegen, wie im folgenden Codebeispiel dargestellt.  
  
```  
workflowServiceHost.DurableInstancingOptions.InstanceStore = sqlInstanceStoreObject;  
```  
  
## <a name="enabling-persistence-for-was-hosted-workflow-services-that-use-the-workflowservicehost-using-a-configuration-file"></a>Aktivieren der Persistenz für per WAS gehostete Workflowdienste, die WorkflowServiceHost verwenden, mithilfe einer Konfigurationsdatei  
 Sie können die Persistenz für selbst gehostete oder per WAS (Windows Process Activation Service) gehostete Workflowdienste mithilfe einer Konfigurationsdatei aktivieren. Ein per WAS gehosteter Workflowdienst verwendet WorkflowServiceHost, wie selbst gehostete Workflowdienste dies auch tun.  
  
 Die `SqlWorkflowInstanceStoreBehavior`, ein Dienstverhalten, mit dem können Sie bequem ändern die [SQL-Workflowinstanzspeicher](../../../docs/framework/windows-workflow-foundation/sql-workflow-instance-store.md) Eigenschaften über die XML-Konfiguration. Verwenden Sie für per WAS gehostete Workflowdienste die Datei "Web.config". Im folgenden Konfigurationsbeispiel wird gezeigt, wie Sie den SQL-Workflowinstanzspeicher konfigurieren, indem Sie das `sqlWorkflowInstanceStore`-Verhaltenselement in einer Konfigurationsdatei verwenden.  
  
```xml  
<serviceBehaviors>  
    <behavior name="">  
        <sqlWorkflowInstanceStore   
                    connectionString="Data Source=(local);Initial Catalog=DefaultPersistenceProviderDb;Integrated Security=True;Async=true"  
                    instanceEncodingOption="GZip | None"  
                    instanceCompletionAction="DeleteAll | DeleteNothing"  
                    instanceLockedExceptionAction="NoRetry | BasicRetry |AggressiveRetry"  
                    hostLockRenewalPeriod="00:00:30"   
                    runnableInstancesDetectionPeriod="00:00:05">  
  
        <sqlWorkflowInstanceStore/>  
    </behavior>  
</serviceBehaviors>  
```  
  
 Falls Sie keine Werte für die `connectionString`- oder `connectionStringName`-Eigenschaft festlegen, verwendet der SQL-Workflowinstanzspeicher die standardmäßige Verbindungszeichenfolge `DefaultSqlWorkflowInstanceStoreConnectionString`.  
  
 Wenn `SqlWorkflowInstanceStoreBehavior` angewendet wird, wird `DurableInstancingOptions.InstanceStore` auf dem `WorkflowServiceHost` auf das `SqlWorkflowInstanceStore`-Element festgelegt, das anhand der Konfigurationswerte erstellt wurde. Dies können Sie auch programmgesteuert erreichen, indem Sie `SqlWorkflowInstanceStore` mit `WorkflowServiceHost` und ohne das Dienstverhaltenelement verwenden.  
  
```  
workflowServiceHost.DurableInstancingOptions.InstanceStore = sqlInstanceStoreObject;  
```  
  
> [!IMPORTANT]
>  Es wird empfohlen, keine vertraulichen Informationen wie Benutzernamen und Kennwörter in der Datei "Web.config" zu speichern. Wenn Sie vertrauliche Informationen in der Datei "Web.config" speichern, sollten Sie den Zugriff auf die Datei "Web.config" mit Dateisystem-ACLs (Zugriffssteuerungslisten) sichern. Darüber hinaus können sichern Sie auch die Konfigurationswerte innerhalb einer Konfigurationsdatei wie im erwähnt [Verschlüsseln von Informationen mithilfe von geschützten Konfiguration](http://go.microsoft.com/fwlink/?LinkId=178419).  
  
### <a name="machineconfig-elements-related-to-the-sql-workflow-instance-store-feature"></a>Auf die Funktion „SQL-Workflowinstanzspeicher“ bezogene Elemente von „Machine.config“  
 Die [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)]-Installation fügt die folgenden Elemente, die sich auf die Funktion "SQL-Workflowinstanzspeicher" beziehen, der Datei "Machine.config" hinzu:  
  
-   Fügt der Datei "Machine.config" das folgende Verhaltenserweiterungselement hinzu, damit Sie das <`sqlWorkflowInstanceStore`>-Dienstverhaltenelement in der Konfigurationsdatei verwenden können, um die Persistenz für die Dienste zu konfigurieren.  
  
    ```xml  
    <configuration>  
        <system.serviceModel>  
            <extensions>  
                <behaviorExtensions>  
                    <add name="sqlWorkflowInstanceStore" type="System.Activities.DurableInstancing.SqlWorkflowInstanceStoreElement, System.Activities.DurableInstancing, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35" />  
                </behaviorExtensions>  
            </extensions>  
        <system.serviceModel>  
    <configuration>  
    ```
