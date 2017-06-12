---
title: "UI Automation Support for the ComboBox Control Type | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "control types, Combo Box"
  - "UI Automation, Combo Box control type"
  - "ComboBox controls"
ms.assetid: bb321126-4770-41da-983a-67b7b89d45dd
caps.latest.revision: 23
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 23
---
# UI Automation Support for the ComboBox Control Type
> [!NOTE]
>  Diese Dokumentation ist für .NET Framework\-Entwickler vorgesehen, die die verwalteten [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Klassen verwenden möchten, die im <xref:System.Windows.Automation>\-Namespace definiert sind. Aktuelle Informationen zur [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] finden Sie auf der Seite zur [Windows\-Automatisierungs\-API: UI\-Automatisierung](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 Dieses Thema enthält Informationen über [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Unterstützung für den Steuerelementtyp „ComboBox“. In [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] umfasst ein Steuerelementtyp eine Reihe von Bedingungen, die ein Steuerelement erfüllen muss, damit die <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty>\-Eigenschaft verwendet werden kann. Die Bedingungen schließen bestimmte Richtlinien für [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Struktur, [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Eigenschaftswerte, Steuerelementmuster und [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Ereignisse ein.  
  
 Ein Kombinationsfeld ist ein Listenfeld, das mit einem statischen Steuerelement oder einem Bearbeitungssteuerelement kombiniert ist und das momentan ausgewählte Element im Listenfeldbereich des Kombinationsfelds anzeigt. Der Listenfeldbereich des Steuerelements wird dauerhaft oder nur dann angezeigt, wenn der Dropdownpfeil \(der eine Schaltfläche ist\) neben dem Steuerelement ausgewählt wurde. Wenn das Auswahlfeld ein Bearbeitungssteuerelement ist, kann der Benutzer Informationen eingeben, die in der Liste nicht vorhanden sind. Andernfalls kann er nur Elemente in der Liste auswählen.  
  
 In den folgenden Abschnitten werden die [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Struktur, Eigenschaften, Steuerelementmuster und Ereignisse definiert, die für den ComboBox\-Steuerelementtyp erforderlich sind. Die [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Anforderungen gelten für alle Kombinationsfeld\-Steuerelemente, egal ob [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)], [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)] oder [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)].  
  
<a name="Required_UI_Automation_Tree_Structure"></a>   
## Erforderliche Benutzeroberflächenautomatisierungs\-Struktur  
 In der folgenden Tabelle werden die Steuerelementansicht und die Inhaltsansicht der [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Struktur für Kombinationsfeld\-Steuerelemente sowie die möglichen Inhalte jeder Ansicht beschrieben. Weitere Informationen über die [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Struktur finden Sie unter [UI Automation Tree Overview](../../../docs/framework/ui-automation/ui-automation-tree-overview.md).  
  
|Steuerelementansicht|Inhaltsansicht|  
|--------------------------|--------------------|  
|ComboBox<br /><br /> -   Bearbeitung \(0 oder 1\)<br />-   Liste \(1\)<br />-   Listenelement \(untergeordnetes Element von Liste; 0 bis viele\)<br />-   Schaltfläche \(1\)|ComboBox<br /><br /> -   Listenelement \(0 bis viele\)|  
  
 Das Bearbeitungssteuerelement in der Steuerelementansicht des Kombinationsfelds ist nur erforderlich, wenn das Kombinationsfeld bearbeitet werden kann, um beliebige Eingaben anzunehmen, wie dies für das Kombinationsfeld im Dialogfeld „Ausführen“ der Fall ist.  
  
<a name="Required_UI_Automation_Properties"></a>   
## Erforderliche Benutzeroberflächenautomatisierungs\-Eigenschaften  
 In der folgenden Tabelle werden die [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Eigenschaften aufgelistet, deren Werte oder Definitionen für Kombinationsfeld\-Steuerelemente besonders relevant sind. Weitere Informationen zu [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Eigenschaften finden Sie unter [UI Automation Properties for Clients](../../../docs/framework/ui-automation/ui-automation-properties-for-clients.md).  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Eigenschaft|Wert|Notizen|  
|----------------------------------------------------------------------------------------|----------|-------------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|Siehe Hinweise.|Der Wert dieser Eigenschaft muss für alle Steuerelemente in einer Anwendung eindeutig sein.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|Siehe Hinweise.|Das äußere Rechteck, das das gesamte Steuerelement enthält.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|Siehe Hinweise.|Unterstützt, wenn es ein umschließendes Rechteck gibt. Wenn nicht auf jeden Punkt innerhalb des umschließenden Rechtecks geklickt werden kann, und Sie spezielle Treffertests ausführen, setzen Sie die Eigenschaft außer Kraft, und stellen Sie dann einen klickbaren Punkt bereit.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|ComboBox|Dieser Wert gilt für alle [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]\-Frameworks.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.HelpTextProperty>|Siehe Hinweise.|Der Hilfetext für ein Kombinationsfeld\-Steuerelement sollte erläutern, warum der Benutzer aufgefordert wird, eine Option im Kombinationsfeld auszuwählen. Der Text ist mit den in einer QuickInfo angezeigten Informationen vergleichbar. Beispiel: „Wählen Sie ein Element aus, um die Anzeigeauflösung des Bildschirms festzulegen.“|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|True|Kombinationsfeld\-Steuerelemente sind immer in der Inhaltsansicht der [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Struktur enthalten.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|Kombinationsfeld\-Steuerelemente sind immer in der Steuerelementansicht der [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Struktur enthalten.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|True|Kombinationsfeld\-Steuerelemente machen einen Satz von Elementen aus einem Auswahlcontainer verfügbar. Das Kombinationsfeld\-Steuerelement \(ComboBox\) kann den Tastaturfokus erhalten, aber wenn ein Benutzeroberflächenautomatisierungs\-Client den Fokus auf ein Kombinationsfeld setzt, können ggf. alle Elemente in der Unterstruktur des Kombinationsfelds den Fokus erhalten.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|Siehe Hinweise.|Ein Kombinationsfeld\-Steuerelement hat normalerweise eine statische Textbezeichnung, auf die diese Eigenschaft verweist.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|„Kombinationsfeld“|Lokalisierte Zeichenfolge für den Steuerelementtyp „CombBox“.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|Siehe Hinweise.|Das Kombinationsfeld\-Steuerelement erhält seinen Namen normalerweise aus einem statischen Textsteuerelement.|  
  
<a name="Required_UI_Automation_Control_Patterns"></a>   
## Erforderliche Benutzeroberflächenautomatisierungs\-Steuerelementmuster  
 Die folgende Tabelle enthält die [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Steuerelementmuster, die von allen Kombinationsfeld\-Steuerelementen unterstützt werden müssen. Weitere Informationen zu Steuerelementmustern finden Sie unter [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md).  
  
|Steuerelementmuster|Unterstützung|Notizen|  
|-------------------------|-------------------|-------------|  
|<xref:System.Windows.Automation.Provider.IExpandCollapseProvider>|Ja|Ein Kombinationsfeld\-Steuerelement muss immer eine Dropdownschaltfläche enthalten, damit es ein Kombinationsfeld ist.|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider>|Ja|Zeigt die aktuelle Auswahl im Kombinationsfeld an. Diese Unterstützung wird an das Listenfeld unter dem Kombinationsfelds delegiert.|  
|<xref:System.Windows.Automation.Provider.IValueProvider>|Variabel|Wenn das Kombinationsfeld beliebige Textwerte aufnehmen kann, muss das Value\-Muster unterstützt werden. Dieses Muster eröffnet die Möglichkeit, den Zeichenfolgeninhalt des Kombinationsfelds programmgesteuert festzulegen. Wenn das Value\-Muster nicht unterstützt wird, weist dies darauf hin, dass der Benutzer aus den Listenelementen in der Unterstruktur des Kombinationsfelds auswählen muss.|  
|<xref:System.Windows.Automation.Provider.IScrollProvider>|Nie|Das Scroll\-Muster wird nie direkt für ein Kombinationsfeld unterstützt. Es wird unterstützt, wenn in einem Listenfeld, das in einem Kombinationsfeld enthalten ist, gescrollt werden kann. Es wird möglicherweise nur unterstützt, wenn das Listenfeld auf dem Bildschirm sichtbar ist.|  
  
<a name="Required_Events"></a>   
## Erforderliche Ereignisse  
 In der folgenden Tabelle sind die [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Ereignisse aufgeführt, die von allen Kombinationsfeld\-Steuerelementen unterstützt werden müssen. Weitere Informationen zu Ereignissen finden Sie unter [UI Automation Events Overview](../../../docs/framework/ui-automation/ui-automation-events-overview.md).  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Ereignis|Unterstützung|Notizen|  
|-------------------------------------------------------------------------------------|-------------------|-------------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|Erforderlich|Keine|  
|Durch geänderte <xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>\-Eigenschaft ausgelöstes Ereignis.|Erforderlich|Keine|  
|Durch geänderte <xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty>\-Eigenschaft ausgelöstes Ereignis.|Erforderlich|Keine|  
|Durch geänderte <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty>\-Eigenschaft ausgelöstes Ereignis.|Erforderlich|Keine|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|Erforderlich|Keine|  
|Durch geänderte <xref:System.Windows.Automation.ExpandCollapsePatternIdentifiers.ExpandCollapseStateProperty>\-Eigenschaft ausgelöstes Ereignis.|Erforderlich|Keine|  
|Durch geänderte <xref:System.Windows.Automation.ValuePatternIdentifiers.ValueProperty>\-Eigenschaft ausgelöstes Ereignis.|Variabel|Wenn das Steuerelement das Value\-Muster unterstützt, muss es dieses Ereignis unterstützen.|  
  
## Siehe auch  
 <xref:System.Windows.Automation.ControlType.ComboBox>   
 [UI Automation Control Types Overview](../../../docs/framework/ui-automation/ui-automation-control-types-overview.md)   
 [UI Automation Overview](../../../docs/framework/ui-automation/ui-automation-overview.md)