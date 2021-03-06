---
title: Markuperweiterungen und WPF-XAML
ms.date: 03/30/2017
helpviewer_keywords:
- brace character [WPF]
- Binding markup extensions [WPF]
- RelativeSource markup extensions [WPF]
- XAML [WPF], markup extensions
- markup extensions [WPF]
- nesting extension syntax [WPF]
- curly brace characters ({})
- TemplateBinding markup extensions [WPF]
- StaticResource markup extensions [WPF]
- literal curly brace characters ({})
- characters [WPF], curly brace
- DynamicResource markup extensions [WPF]
ms.assetid: 618dc745-8b14-4886-833f-486d2254bb78
ms.openlocfilehash: f18a369157c1e37411a3c8d8b6dfcce99bc347c6
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="markup-extensions-and-wpf-xaml"></a>Markuperweiterungen und WPF-XAML
Dieses Thema bietet eine Einführung das Konzept der Markuperweiterungen für XAML und enthält eine Erläuterung der Syntaxregeln, des Zweck und des zugrunde liegenden Klassenobjektmodels. Markuperweiterungen sind eine allgemeine Funktion der XAML-Sprache und der .NET-Implementierung von XAML-Diensten. In diesem Thema werden speziell Markuperweiterungen zur Verwendung in WPF XAML beschrieben.  
  
  
<a name="XAML_Processors_and_Markup_Extensions"></a>   
## <a name="xaml-processors-and-markup-extensions"></a>XAML-Prozessoren und Markuperweiterungen  
 Im Allgemeinen kann ein XAML-Parser einen Attributwert entweder als Literalzeichenfolge interpretieren, die in eine Primitive konvertiert werden kann, oder auf bestimmte Weise in ein Objekt konvertieren. Eine Möglichkeit ist das Verweisen auf einen Typkonverter; dies wird im Thema [TypeConverter und XAML](../../../../docs/framework/wpf/advanced/typeconverters-and-xaml.md) dokumentiert. Bestimmte Szenarios erfordern jedoch ein anderes Verhalten. Ein XAML-Prozessor kann z.B. angewiesen werden, dass der Wert eines Attributs nicht zu einem neuen Objekt im Objektdiagramm führen soll. Stattdessen soll das Attribut ein Objektdiagramm ergeben, das auf ein bereits erstelltes Objekt in einem anderen Teil des Diagramms oder auf ein statisches Objekt verweist. Ein anderes Szenario ist, dass ein XAML-Prozessor angewiesen werden kann, Syntax zu verwenden, die für den Konstruktor eines Objekts nicht standardmäßige Argumente bereitstellt. Bei derartigen Szenarios eine Markuperweiterung die Lösung sein.  
  
<a name="Basic_Markup_Extension_Syntax"></a>   
## <a name="basic-markup-extension-syntax"></a>Grundlegende Markuperweiterungssyntax  
 Eine Markuperweiterung kann zur Bereitstellung von Werten für Eigenschaften zur Verwendung von Attributen, für Eigenschaften zur Verwendung von Eigenschaftenelementen oder für beides implementiert werden.  
  
 Wenn die Markuperweiterungssequenz zum Bereitstellen eines Attributwerts verwendet wird, wird dies durch die Verwendung von öffnenden und schließenden geschweiften Klammern ({ und }) in der Syntax für den XAML-Prozessor kenntlich gemacht. Das Zeichenfolgentoken, das unmittelbar auf die öffnende geschweifte Klammer folgt, bestimmt den Typ der Markuperweiterung.  
  
 Bei Verwendung in der Eigenschaftenelementsyntax entspricht das Erscheinungsbild der Markuperweiterung einem Element, das zum Bereitstellen eines Eigenschaftenelementwerts verwendet wird: eine XAML-Elementdeklaration, die auf die Markuperweiterungsklasse als Element verweist und von spitzen Klammern (<>) umschlossen ist.  
  
<a name="XAML_Defined_Markup_Extensions"></a>   
## <a name="xaml-defined-markup-extensions"></a>XAML-definierte Markuperweiterungen  
 Es gibt mehrere Markuperweiterungen, die nicht spezifisch für die WPF-Implementierung von XAML gelten, sondern Implementierungen für Interna oder Funktionen von XAML als Sprache sind. Diese Markuperweiterungen werden als Teil der allgemeinen .NET Framework-XAML-Dienste in der System.Xaml-Assembly implementiert und sind im XAML-Sprachnamespace enthalten. Im Hinblick auf die allgemeine Markupverwendung sind diese Markuperweiterungen in der Regel durch das `x:`-Präfix in der Verwendung identifizierbar. Die <xref:System.Windows.Markup.MarkupExtension> Basisklasse (auch in "System.xaml" definiert) enthält das Muster, das alle Markuperweiterungen verwendet werden soll, um in XAML-Readern und XAML-Writer, einschließlich in WPF-XAML unterstützt werden.  
  
-   `x:Type` stellt das <xref:System.Type> -Objekt für den benannten Typ bereit. Diese Funktion wird am häufigsten in Stilen und Vorlagen verwendet. Weitere Informationen finden Sie unter [x:Type-Markuperweiterung](../../../../docs/framework/xaml-services/x-type-markup-extension.md).  
  
-   `x:Static` erzeugt statische Werte. Die Werte stammen aus Wert-Typ-Codeentitäten, die nicht direkt dem Typ eines Zieleigenschaftswerts entsprechen, jedoch diesem Typ entsprechend ausgewertet werden können. Weitere Informationen finden Sie unter [x:Statische Markuperweiterung](../../../../docs/framework/xaml-services/x-static-markup-extension.md).  
  
-   `x:Null` gibt `null` als Wert für eine Eigenschaft an und kann für Attribute oder Eigenschaftenelementwerte verwendet werden. Weitere Informationen finden Sie unter [x:Null-Markuperweiterung](../../../../docs/framework/xaml-services/x-null-markup-extension.md).  
  
-   `x:Array` bietet Unterstützung für die Erstellung von allgemeinen Arrays in XAML-Syntax, wenn die Auflistungsunterstützung von WPF-Basiselementen und Steuerelementmodellen bewusst nicht verwendet wird. Weitere Informationen finden Sie unter [x:Array-Markuperweiterung](../../../../docs/framework/xaml-services/x-array-markup-extension.md).  
  
> [!NOTE]
>  Das `x:`-Präfix wird für die typische XAML-Namespacezuordnung der systeminternen XAML-Sprache im Stammelement einer XAML-Datei oder Produktion verwendet. Beispielsweise initiieren die Visual Studio-Vorlagen für WPF-Anwendungen eine XAML-Datei, die mithilfe dieser `x:` Zuordnung. Sie können ein anderes Präfixtoken in Ihrer eigenen XAML-Namespacezuordnung auswählen, dieser Dokumentation wird jedoch die `x:`-Standardzuordnung für die Identifizierung der Entitäten zugrunde gelegt, die als Teil des XAML-Sprachnamespace definiert sind (im Gegensatz zu einem standardmäßigen WPF-Namespace oder anderen XAML-Namespaces, die keinem bestimmten Framework zugeordnet sind).  
  
<a name="WPF_Specific_Markup_Extensions"></a>   
## <a name="wpf-specific-markup-extensions"></a>WPF-spezifische Markuperweiterungen  
 Bei der WPF-Programmierung werden am häufigsten die Markuperweiterungen mit Unterstützung für Ressourcenverweise (`StaticResource` und `DynamicResource`), und mit Unterstützung für Datenbindung verwendet (`Binding`).  
  
-   `StaticResource` stellt einen Wert für eine Eigenschaft bereit, indem der Wert einer bereits definierten Ressource ersetzt wird. Schließlich wird eine `StaticResource`-Auswertung zur der XAML-Ladezeit vorgenommen, die während der tatsächlichen Laufzeit keinen Zugriff auf das Objektdiagramm hat. Weitere Informationen finden Sie unter [StaticResource-Markuperweiterung](../../../../docs/framework/wpf/advanced/staticresource-markup-extension.md)  
  
-   `DynamicResource` stellt einen Wert für eine Eigenschaft bereit, indem dieser Wert als Laufzeitverweis auf eine Ressource verwendet wird. Ein dynamischer Ressourcenverweis erzwingt jedes Mal eine neue Suche, wenn auf eine solche Ressource zugegriffen wird und diese zur Laufzeit Zugriff auf das Objektdiagramm hat. Um diesen Zugriff abzurufen, wird das `DynamicResource` Konzept von Abhängigkeitseigenschaften im WPF-Eigenschaftensystem und ausgewerteten Ausdrücken unterstützt. Daher kann `DynamicResource` nur für ein Abhängigkeitseigenschaftsziel verwendet werden. Weitere Informationen finden Sie unter [DynamicResource-Markuperweiterung](../../../../docs/framework/wpf/advanced/dynamicresource-markup-extension.md)  
  
-   `Binding` stellt einen datengebundenen Wert für eine Eigenschaft bereit, indem der Datenkontext verwendet wird, der zur Laufzeit für das übergeordnete Objekt gilt. Diese Markuperweiterung ist relativ komplex, da eine komplexe Inlinesyntax für die Angabe einer Datenbindung aktiviert wird. Weitere Informationen finden Sie unter [Binding als Markuperweiterung](../../../../docs/framework/wpf/advanced/binding-markup-extension.md).  
  
-   `RelativeSource` bietet Informationen zur Quellobjekt ein <xref:System.Windows.Data.Binding> können, die mehrere mögliche Beziehungen in der Laufzeit-Objektstruktur navigieren. Hierdurch werden spezielle Quellbezüge für Bindungen bereitgestellt, die ohne vollständige Kenntnis der umgebenden Objektstruktur in Mehrzweckvorlagen oder in Code erstellt werden. Weitere Informationen finden Sie unter [RelativeSource-Markuperweiterungen](../../../../docs/framework/wpf/advanced/relativesource-markupextension.md).  
  
-   `TemplateBinding` ermöglicht die Verwendung von Vorlage-Eigenschaftswerten in Steuerelementvorlagen, die von den durch das Objektmodell definierten Eigenschaften der Klasse stammen, die die Vorlage verwenden werden. Dies bedeutet, dass die Eigenschaft in der Vorlagendefinition auf einen Kontext zugreifen kann, der erst vorhanden ist, wenn die Vorlage angewendet wird. Weitere Informationen finden Sie unter [TemplateBinding Markuperweiterung](../../../../docs/framework/wpf/advanced/templatebinding-markup-extension.md). Weitere Informationen über die praktische Verwendung von `TemplateBinding`, finden Sie unter [Beispiel zum Formatieren mit ControlTemplates](http://go.microsoft.com/fwlink/?LinkID=160041).  
  
-   `ColorConvertedBitmap` unterstützt ein relativ komplexes Bildverarbeitungsszenario. Weitere Informationen finden Sie unter [ColorConvertedBitmap-Markuperweiterung](../../../../docs/framework/wpf/advanced/colorconvertedbitmap-markup-extension.md)  
  
-   `ComponentResourceKey` und `ThemeDictionary` unterstützen Aspekte der Ressourcensuche, insbesondere für Ressourcen und Designs, mit benutzerdefinierten Steuerelementen enthalten sind. Weitere Informationen finden Sie unter [ComponentResourceKey-Markuperweiterung](../../../../docs/framework/wpf/advanced/componentresourcekey-markup-extension.md), [ThemeDictionary-Markuperweiterung](../../../../docs/framework/wpf/advanced/themedictionary-markup-extension.md), oder [Übersicht über das Erstellen von Steuerelementen](../../../../docs/framework/wpf/controls/control-authoring-overview.md).  
  
<a name="StarExtension"></a>   
## <a name="extension-classes"></a>*Erweiterungsklassen  
 Für die allgemeine XAML-Sprache und WPF-spezifischen Markuperweiterungen wird das Verhalten der einzelnen Markuperweiterungen für einen XAML-Prozessor über identifiziert eine `*Extension` von abgeleitete Klasse <xref:System.Windows.Markup.MarkupExtension>, und stellt eine Implementierung von der <xref:System.Windows.Markup.StaticExtension.ProvideValue%2A> Methode. Diese für jede Erweiterung verwendete Methode stellt das Objekt bereit, das bei der Auswertung der Markuperweiterung zurückgegeben wird Das zurückgegebene Objekt wird normalerweise auf Grundlage der verschiedenen Zeichenfolgentoken ausgewertet, die an die Markuperweiterung übergeben werden.  
  
 Z. B. die <xref:System.Windows.StaticResourceExtension> Klasse stellt die Entwurfsoberfläche Implementierung des tatsächlichen Ressourcensuche, damit seine <xref:System.Windows.Markup.MarkupExtension.ProvideValue%2A> Implementierung gibt das Objekt, das angefordert wird, mit der Eingabe dieser bestimmten Implementierung wird eine Zeichenfolge, die verwendet wird, zurück. Suchen Sie die Ressource durch seine `x:Key`. Ein großer Teil dieser Implementierungsdetails ist nicht von Bedeutung, wenn Sie eine bestehende Markuperweiterung verwenden.  
  
 Einige Markuperweiterungen verwenden keine Zeichenfolgentokenargumente. Dies ist darauf zurückzuführen, dass sie einen statischen oder konsistenten Wert zurückgeben, oder darauf, dass der Kontext zum Bestimmen des zurückzugebenden Werts mit einem der durch den `serviceProvider`-Parameter übergebenen Dienste verfügbar ist.  
  
 Das `*Extension`-Namensmuster dient der besseren Übersichtlichkeit und Konsistenz. Es ist nicht erforderlich, damit ein XAML-Prozessor diese Klasse als Unterstützung für eine Markuperweiterung identifiziert. Solange der Codebasis "System.xaml" enthält und .NET Framework-XAML-dienstimplementierungen verwendet werden, alle ist erforderlich, erkannt werden kann, wie eine XAML-Markuperweiterung Ableitung <xref:System.Windows.Markup.MarkupExtension> und um eine Konstruktionssyntax zu unterstützen. WPF definiert Markup Erweiterung Aktivierung von Klassen, die nicht befolgt werden die `*Extension` Muster, z. B. benennen <xref:System.Windows.Data.Binding>. Der Grund hierfür ist normalerweise, dass die Klasse Szenarios unterstützt, die über die reine Unterstützung von Markuperweiterungen hinausgehen. Im Fall von <xref:System.Windows.Data.Binding>, dass die Klasse zur Laufzeit Zugriff auf Methoden und Eigenschaften des Objekts für Szenarien unterstützt, die nichts mit XAML zu tun haben.  
  
### <a name="extension-class-interpretation-of-initialization-text"></a>Erweiterungsklasse – Interpretation der Initialisierungstext  
 Die Zeichenfolgentoken, die auf den Namen der Markuperweiterung folgen und sich innerhalb der Klammern befinden, werden von einem XAML-Prozessor auf eine der folgenden Arten interpretiert:  
  
-   Ein Komma fungiert immer als Trennzeichen einzelner Token.  
  
-   Wenn die einzelnen getrennten Token keine Gleichheitszeichen enthalten, wird jedes Token als Konstruktorargument behandelt. Jeder Konstruktorparameter muss als Typ angegeben werden, der von der Signatur erwartet wird, und die Angabe muss in der von der Signatur erwarteten Reihenfolge erfolgen.  
  
    > [!NOTE]
    >  Ein XAML-Prozessor muss den Konstruktor aufrufen, der der Argumentanzahl der Anzahl von Paaren entspricht. Wenn Sie eine benutzerdefinierte Markuperweiterung implementieren, dürfen Sie aus diesem Grund nicht mehrere Parameter mit derselben Argumentanzahl bereitstellen. Das Verhalten eines XAML-Prozessors, wenn mehrere Konstruktorpfade der Markuperweiterung mit derselben Parameteranzahl vorhanden sind, ist nicht definiert. Sie sollten jedoch davon ausgehen, dass ein XAML-Prozessor eine Ausnahme auslösen kann, wenn diese Situation in den Typdefinitionen der Markuperweiterung vorliegt.  
  
-   Wenn die einzelnen Token Gleichheitszeichen enthalten, ruft der XAML-Prozessor zuerst den Standardkonstruktor für die Markuperweiterung auf. Dann wird jedes Name=Wert-Paar als in der Markuperweiterung vorhandener Eigenschaftenname und als Wert interpretiert, der der Eigenschaft zuzuweisen ist.  
  
-   Wenn in einer Markuperweiterung ein paralleles Ergebnis zwischen dem Konstruktorverhalten und dem Verhalten der Eigenschafteneinstellung vorliegt, können Sie zwischen den Verhalten wählen. Wenn in einer Markuperweiterung ein paralleles Ergebnis zwischen dem Konstruktorverhalten und dem Verhalten der Eigenschafteneinstellung vorliegt, können Sie zwischen den Verhalten wählen. Die Verwendung von *Eigenschaft*`=`*Wert*-Paaren mit mehreren festlegbaren Eigenschaften für Markuperweiterungen ist gängiger, da hierbei ein geringeres Risiko besteht, Konstruktorparameter versehentlich zu vertauschen. (Bei der Angabe von Eigenschaft=Wert-Paaren spielt die Reihenfolge der Eigenschaften keine Rolle). Des Weiteren ist nicht garantiert, dass eine Markuperweiterung einen Konstruktorparameter angibt, der alle festlegbaren Eigenschaften festlegt. Beispielsweise <xref:System.Windows.Data.Binding> ist eine Markuperweiterung, viele Eigenschaften, die durch die Erweiterung in festlegbar sind *Eigenschaft*`=`*Wert* Formular jedoch <xref:System.Windows.Data.Binding> unterstützt nur zwei Konstruktoren: einen Standardkonstruktor und einen, der einen Anfangspfad festlegt.  
  
-   Ein Komma kann nicht ohne Vorschub als Literalzeichen an eine Markuperweiterung übergeben werden.  
  
<a name="EscapeSequences"></a>   
## <a name="escape-sequences-and-markup-extensions"></a>Escapesequenzen und Markuperweiterungen  
 Bei der Attributbehandlung in einem XAML-Prozessor werden geschweifte Klammern als Bezeichner für Markuperweiterungssequenzen verwendet. Falls erforderlich, können Sie geschweifte Klammern als Literalzeichen angeben, indem Sie eine Escapesequenz in Form eines leeren Paars geschweifter Klammern gefolgt von der literalen geschweiften Klammer angeben. Finden Sie unter [ {} Escapesequenz - Markuperweiterung](../../xaml-services/escape-sequence-markup-extension.md).  
  
<a name="Nesting"></a>   
## <a name="nesting-markup-extensions-in-xaml-usage"></a>Schachtelung von Markuperweiterungen in der XAML-Verwendung  
 Schachtelung mehrerer Markuperweiterungen wird unterstützt, und jeder Markuperweiterung wird tiefsten zuerst ausgewertet. Betrachten Sie z.B. die folgende Syntax:  
  
```  
<Setter Property="Background"  
  Value="{DynamicResource {x:Static SystemColors.ControlBrushKey}}" />  
```  
  
 Die `x:Static`-Anweisung wird hier zuerst ausgewertet und gibt eine Zeichenfolge zurück. Diese Zeichenfolge wird dann als Argument für `DynamicResource` verwendet.  
  
## <a name="markup-extensions-and-property-element-syntax"></a>Markuperweiterungen und Eigenschaftenelementsyntax  
 Bei Verwendung als Objektelement, das in einen Eigenschaftenelementwert geladen wird, ist eine Markuperweiterungsklasse visuell nicht von regulären typgestützten Objekten zu unterscheiden, die in XAML verwendet werden können. In diesem Fall besteht der praktische Unterschied zwischen einem typischen Objektelement und einer Markuperweiterung darin, dass die Markuperweiterung entweder als typisierter Wert ausgewertet oder als Ausdruck verzögert wird. Aus diesem Grund unterscheiden sich die Mechanismen für mögliche Typfehler bei Eigenschaftswerten für die Markuperweiterung. Dies ist mit der Behandlung einer Eigenschaft mit später Bindung in anderen Programmiermodellen vergleichbar. Ein normales Objektelement wird beim Analysieren des XAML hinsichtlich der Typübereinstimmung mit der von ihm festgelegten Zieleigenschaft ausgewertet.  
  
 Die meisten Markuperweiterungen würden keinen Inhalt oder weitere Eigenschaftenelementsyntax aufweisen, wenn sie in der Objektelementsyntax in ein Eigenschaftenelement geladen werden. Deshalb würden Sie das Objektelementtag schließen und keine untergeordneten Elemente bereitstellen. Wenn ein Objektelement von einem XAML-Prozessor erkannt wird, wird der Konstruktor für diese Klasse aufgerufen, die das aus dem analysierten Element erstellte Objekt instanziiert. Dies gilt auch für Markuperweiterungsklassen. Wenn Sie die Markuperweiterung in Objektelementsyntax verwenden möchten, müssen Sie einen Standardkonstruktor angeben. Einige vorhandene Markuperweiterungen verfügen über mindestens einen erforderlichen Eigenschaftswert, der für die effektive Initialisierung angegeben werden muss. Wenn dies der Fall ist, wird dieser Eigenschaftswert in der Regel als Eigenschaftenattribut für das Objektelement angegeben. Markuperweiterungen mit erforderlichen Eigenschaften (sowie die Namen dieser Eigenschaften) werden auf den Referenzseiten [XAML-Namespace (x:) Sprachfeatures](../../../../docs/framework/xaml-services/xaml-namespace-x-language-features.md) und [WPF-XAML-Erweiterungen](../../../../docs/framework/wpf/advanced/wpf-xaml-extensions.md) aufgeführt. Des Weiteren wird auf den Referenzseiten darauf hingewiesen, wenn Objektelementsyntax oder Attributsyntax von einer Markuperweiterung nicht unterstützt werden. Ein wichtiger Fall ist [X: Array-Markuperweiterung](../../../../docs/framework/xaml-services/x-array-markup-extension.md), die Attributsyntax nicht unterstützt, da der Inhalt des Arrays innerhalb der Tags als Inhalt angegeben werden muss. Die Arrayinhalte werden als allgemeine Objekte behandelt, sodass kein Standardtypkonverter für das Attribut zulässig ist. Außerdem erfordert [X: Array-Markuperweiterung](../../../../docs/framework/xaml-services/x-array-markup-extension.md) einen `type`-Parameter.  
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht über XAML (WPF)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)  
 [Sprachfunktionen des XAML-Namespace (x:)](../../../../docs/framework/xaml-services/xaml-namespace-x-language-features.md)  
 [WPF-XAML-Erweiterungen](../../../../docs/framework/wpf/advanced/wpf-xaml-extensions.md)  
 [StaticResource-Markuperweiterung](../../../../docs/framework/wpf/advanced/staticresource-markup-extension.md)  
 [Bindung als Markuperweiterung](../../../../docs/framework/wpf/advanced/binding-markup-extension.md)  
 [DynamicResource-Markuperweiterung](../../../../docs/framework/wpf/advanced/dynamicresource-markup-extension.md)  
 [x:Type-Markuperweiterung](../../../../docs/framework/xaml-services/x-type-markup-extension.md)
