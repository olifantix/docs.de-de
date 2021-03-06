---
title: 'Vorgehensweise: Paralleles Erstellen mehrerer Webanforderungen mit Async und Await (C#)'
ms.custom: 
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
ms.assetid: 19745899-f97a-4499-a7c7-e813d1447580
caps.latest.revision: 
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 509f9e690a5157c2d80ba9726354ce57a9d7ff26
ms.sourcegitcommit: cec0525b2121c36198379525e69aa5388266db5b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/23/2018
---
# <a name="how-to-make-multiple-web-requests-in-parallel-by-using-async-and-await-c"></a>Vorgehensweise: Paralleles Erstellen mehrerer Webanforderungen mit Async und Await (C#)
In einer asynchronen Methode werden Aufgaben gestartet, wenn sie erstellt werden. Der [await](../../../../csharp/language-reference/keywords/await.md)-Operator wird auf die Aufgabe an dem Punkt in der Methode angewendet, an dem die Verarbeitung nicht fortgesetzt werden kann, bis die Aufgabe abgeschlossen ist. Häufig wird eine Aufgabe erwartet, sobald sie erstellt wird, wie das folgende Beispiel zeigt.  
  
```csharp  
var result = await someWebAccessMethodAsync(url);  
```  
  
 Sie können das Erstellen der Aufgabe vom Erwarten der Aufgabe jedoch trennen, wenn das Programm weitere Arbeit durchführen muss, die nicht vom Abschluss der Aufgabe abhängig ist.  
  
```csharp  
// The following line creates and starts the task.  
var myTask = someWebAccessMethodAsync(url);  
  
// While the task is running, you can do other work that doesn't depend  
// on the results of the task.  
// . . . . .  
  
// The application of await suspends the rest of this method until the task is complete.  
var result = await myTask;  
```  
  
 Zwischen dem Starten und dem Erwarten einer Aufgabe können Sie andere Aufgaben starten. Die weiteren Aufgaben werden implizit parallel ausgeführt, es werden jedoch keine weiteren Threads erstellt.  
  
 Das folgende Programm startet drei asynchrone Webdownloads und erwartet diese dann in der Reihenfolge, in der sie aufgerufen wurden. Beachten Sie, dass die Aufgaben beim Ausführen des Programms nicht immer in der Reihenfolge abgeschlossen werden, in der sie erstellt und erwartet werden. Sie beginnen mit der Ausführung, wenn sie erstellt werden, und eine oder mehrere Aufgaben werden u. U. abgeschlossen, bevor die Methode die await-Ausdrucke erreicht.  
  
> [!NOTE]
>  Zum Fertigstellen dieses Projekts muss Visual Studio 2012 oder höher sowie .NET Framework 4.5 oder höher auf dem Computer installiert sein.  
  
 Ein weiteren Beispiel, in dem mehrere Aufgaben zur gleichen Zeit gestartet werden, finden Sie unter [Vorgehensweise: Erweitern der asynchronen exemplarischen Vorgehensweise mit Task.WhenAll (C#)](../../../../csharp/programming-guide/concepts/async/how-to-extend-the-async-walkthrough-by-using-task-whenall.md).  
  
 Sie können den Code für dieses Beispiel auf der Seite für [Codebeispiele für Entwickler](https://code.msdn.microsoft.com/Async-Make-Multiple-Web-49adb82e) herunterladen.  
  
### <a name="to-set-up-the-project"></a>So richten Sie das Projekt ein  
  
1.  Führen Sie die folgenden Schritte aus, um eine WPF-Anwendung einzurichten. Ausführliche Anweisungen zu diesen Schritten finden Sie unter [Exemplarische Vorgehensweise: Zugreifen auf das Web mit async und await (C#)](../../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md).  
  
    -   Erstellen Sie eine WPF-Anwendung, die ein Textfeld und eine Schaltfläche enthält. Benennen Sie die Schaltfläche mit `startButton` und das Textfeld mit `resultsTextBox`.  
  
    -   Fügen Sie einen Verweis für <xref:System.Net.Http> hinzu.  
  
    -   Fügen Sie in der Datei „MainWindow.xaml.cs“ ein `using`-Verzeichnis für `System.Net.Http` ein.  
  
### <a name="to-add-the-code"></a>So fügen Sie den Code hinzu  
  
1.  Doppelklicken Sie im Entwurfsfenster „MainWindow.xaml“ auf die Schaltfläche, um den `startButton_Click`-Ereignishandler in „MainWindow.xaml.cs“ zu erstellen.  
  
2.  Kopieren Sie den folgenden Code, und fügen Sie ihn in den Text von `startButton_Click` in „MainWindow.xaml.cs“ ein.  
  
    ```csharp  
    resultsTextBox.Clear();  
    await CreateMultipleTasksAsync();  
    resultsTextBox.Text += "\r\n\r\nControl returned to startButton_Click.\r\n";  
    ```  
  
     Der Code ruft die asynchrone Methode `CreateMultipleTasksAsync` auf, die die Anwendung steuert.  
  
3.  Fügen Sie dem Projekt die folgenden Unterstützungsmethoden hinzu:  
  
    -   `ProcessURLAsync` verwendet eine <xref:System.Net.Http.HttpClient>-Methode, um die Inhalte einer Website als Bytearray herunterzuladen. Die Unterstützungsmethode `ProcessURLAsync` wird daraufhin angezeigt und gibt die Länge des Arrays zurück.  
  
    -   `DisplayResults` zeigt die Anzahl von Bytes im Bytearray für jede URL an. Diese Anzeige wird aufgerufen, wenn alle Aufgaben den Download abgeschlossen haben.  
  
     Kopieren Sie die folgenden Methoden, und fügen Sie sie nach dem `startButton_Click`-Ereignishandler in „MainWindow.xaml.cs“ ein.  
  
    ```csharp  
    async Task<int> ProcessURLAsync(string url, HttpClient client)  
    {  
        var byteArray = await client.GetByteArrayAsync(url);  
        DisplayResults(url, byteArray);  
        return byteArray.Length;  
    }  
  
    private void DisplayResults(string url, byte[] content)  
    {  
        // Display the length of each website. The string format   
        // is designed to be used with a monospaced font, such as  
        // Lucida Console or Global Monospace.  
        var bytes = content.Length;  
        // Strip off the "http://".  
        var displayURL = url.Replace("http://", "");  
        resultsTextBox.Text += string.Format("\n{0,-58} {1,8}", displayURL, bytes);  
    }  
    ```  
  
4.  Definieren Sie schließlich die `CreateMultipleTasksAsync`-Methode, die die folgenden Schritte ausführt.  
  
    -   Die Methode deklariert ein `HttpClient`-Objekt, das Sie für den Zugriff auf die <xref:System.Net.Http.HttpClient.GetByteArrayAsync%2A>-Methode in `ProcessURLAsync` benötigen.  
  
    -   Die Methode erstellt und startet drei Aufgaben vom Typ <xref:System.Threading.Tasks.Task%601>, wobei `TResult` eine ganze Zahl ist. Beim Abschließen jeder Aufgabe zeigt `DisplayResults` die URL der Aufgabe sowie die Länge der heruntergeladenen Inhalte an. Da die Aufgaben asynchron ausgeführt werden, kann sich die Reihenfolge, in der die Ergebnisse angezeigt werden, von der Reihenfolge, in der sie deklariert wurden, unterscheiden.  
  
    -   Die Methode erwartet den Abschluss jeder Aufgabe. Jeder `await`-Operator hält die Ausführung von `CreateMultipleTasksAsync` an, bis die erwartete Aufgabe abgeschlossen ist. Der Operator ruft außerdem den Rückgabewert des Aufrufs von `ProcessURLAsync` von jeder abgeschlossenen Aufgabe ab.  
  
    -   Wenn die Aufgaben abgeschlossen und die ganzzahligen Werte abgerufen wurden, werden die Längen der Websites von der Methode summiert, und das Ergebnis wird angezeigt.  
  
     Kopieren Sie die folgende Methode, und fügen Sie sie in Ihre Projektmappe ein.  
  
    ```csharp  
    private async Task CreateMultipleTasksAsync()  
    {  
        // Declare an HttpClient object, and increase the buffer size. The  
        // default buffer size is 65,536.  
        HttpClient client =  
            new HttpClient() { MaxResponseContentBufferSize = 1000000 };  
  
        // Create and start the tasks. As each task finishes, DisplayResults   
        // displays its length.  
        Task<int> download1 =   
            ProcessURLAsync("http://msdn.microsoft.com", client);  
        Task<int> download2 =   
            ProcessURLAsync("http://msdn.microsoft.com/library/hh156528(VS.110).aspx", client);  
        Task<int> download3 =   
            ProcessURLAsync("http://msdn.microsoft.com/library/67w7t67f.aspx", client);  
  
        // Await each task.  
        int length1 = await download1;  
        int length2 = await download2;  
        int length3 = await download3;  
  
        int total = length1 + length2 + length3;  
  
        // Display the total count for the downloaded websites.  
        resultsTextBox.Text +=  
            string.Format("\r\n\r\nTotal bytes returned:  {0}\r\n", total);  
    }  
    ```  
  
5.  Drücken Sie die Taste F5, um das Programm auszuführen, und klicken Sie dann auf die Schaltfläche **Starten** .  
  
     Führen Sie das Programm mehrmals aus, um sicherzustellen, dass die drei Aufgaben nicht immer in derselben Reihenfolge abgeschlossen werden und dass die Reihenfolge, in der sie abgeschlossen werden, nicht notwendigerweise der Reihenfolge entspricht, in der sie erstellt und erwartet werden.  
  
## <a name="example"></a>Beispiel  
 Der folgende Code umfasst das vollständige Beispiel.  
  
```csharp  
using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.Text;  
using System.Threading.Tasks;  
using System.Windows;  
using System.Windows.Controls;  
using System.Windows.Data;  
using System.Windows.Documents;  
using System.Windows.Input;  
using System.Windows.Media;  
using System.Windows.Media.Imaging;  
using System.Windows.Navigation;  
using System.Windows.Shapes;  
  
// Add the following using directive, and add a reference for System.Net.Http.  
using System.Net.Http;  
  
namespace AsyncExample_MultipleTasks  
{  
    public partial class MainWindow : Window  
    {  
        public MainWindow()  
        {  
            InitializeComponent();  
        }  
  
        private async void startButton_Click(object sender, RoutedEventArgs e)  
        {  
            resultsTextBox.Clear();  
            await CreateMultipleTasksAsync();  
            resultsTextBox.Text += "\r\n\r\nControl returned to startButton_Click.\r\n";  
        }  
  
        private async Task CreateMultipleTasksAsync()  
        {  
            // Declare an HttpClient object, and increase the buffer size. The  
            // default buffer size is 65,536.  
            HttpClient client =  
                new HttpClient() { MaxResponseContentBufferSize = 1000000 };  
  
            // Create and start the tasks. As each task finishes, DisplayResults   
            // displays its length.  
            Task<int> download1 =   
                ProcessURLAsync("http://msdn.microsoft.com", client);  
            Task<int> download2 =   
                ProcessURLAsync("http://msdn.microsoft.com/library/hh156528(VS.110).aspx", client);  
            Task<int> download3 =   
                ProcessURLAsync("http://msdn.microsoft.com/library/67w7t67f.aspx", client);  
  
            // Await each task.  
            int length1 = await download1;  
            int length2 = await download2;  
            int length3 = await download3;  
  
            int total = length1 + length2 + length3;  
  
            // Display the total count for the downloaded websites.  
            resultsTextBox.Text +=  
                string.Format("\r\n\r\nTotal bytes returned:  {0}\r\n", total);  
        }  
  
        async Task<int> ProcessURLAsync(string url, HttpClient client)  
        {  
            var byteArray = await client.GetByteArrayAsync(url);  
            DisplayResults(url, byteArray);  
            return byteArray.Length;  
        }  
  
        private void DisplayResults(string url, byte[] content)  
        {  
            // Display the length of each website. The string format   
            // is designed to be used with a monospaced font, such as  
            // Lucida Console or Global Monospace.  
            var bytes = content.Length;  
            // Strip off the "http://".  
            var displayURL = url.Replace("http://", "");  
            resultsTextBox.Text += string.Format("\n{0,-58} {1,8}", displayURL, bytes);  
        }  
    }  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Exemplarische Vorgehensweise: Zugreifen auf das Web mit „async“ und „await“ (C#)](../../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)  
 [Asynchronous Programming with async and await (C#) (Asynchrone Programmierung mit Async und Await (C#))](../../../../csharp/programming-guide/concepts/async/index.md)  
 [Vorgehensweise: Erweitern der asynchronen exemplarischen Vorgehensweise mit Task.WhenAll (C#)](../../../../csharp/programming-guide/concepts/async/how-to-extend-the-async-walkthrough-by-using-task-whenall.md)
