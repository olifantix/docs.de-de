---
title: Implementierung von freigegebenen Verhaltensweisen in der XslTransform-Klasse
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d2758ea1-03f6-47bd-88d2-0fb7ccdb2fab
caps.latest.revision: 
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 98ad31039b5351a7dc4aa3cf033ae8cd0f896b7b
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/23/2017
---
# <a name="implementation-of-discretionary-behaviors-in-the-xsltransform-class"></a>Implementierung von freigegebenen Verhaltensweisen in der XslTransform-Klasse
> [!NOTE]
>  Die <xref:System.Xml.Xsl.XslTransform>-Klasse ist in [!INCLUDE[dnprdnext](../../../../includes/dnprdnext-md.md)] veraltet. Mithilfe der <xref:System.Xml.Xsl.XslCompiledTransform>-Klasse können Sie XSLT-Transformationen (Extensible Stylesheet Language for Transformations) vornehmen. Weitere Informationen finden Sie unter [Verwenden der XslCompiledTransform](../../../../docs/standard/data/xml/using-the-xslcompiledtransform-class.md)-Klasse und [Migrieren von der XslTransform](../../../../docs/standard/data/xml/migrating-from-the-xsltransform-class.md)-Klasse.  
  
 Freigegebene Verhaltensweisen sind die in der W3C-Empfehlung zu XSL-Transformationen (XSLT), Version 1.0 (www.w3.org/TR/xslt), aufgelisteten Verhaltensweisen, bei denen der Implemetierungsanbieter eine von mehreren Optionen zur Behandlung einer bestimmten Situation auswählt. Laut W3C-Empfehlung, Abschnitt 7.3, "Creating Processing Instructions", liegt z. B. ein Fehler vor, wenn durch Instanziierung des Inhalts von `xsl:processing-instruction` außer Textknoten auch andere Knoten erstellt werden. Bei bestimmten Problemen nennt das W3C auch Maßnahmen für den Fall, dass der Prozessor eine Wiederherstellung vom Fehler durchführt. Für das in Abschnitt 7.3 angeführte Problem empfiehlt das W3C, die Knoten einschließlich des Inhalts zu ignorieren, damit die Implementierung von diesem Fehler wiederherstellen kann.  
  
 Daher enthält die folgende Tabelle alle freigegebenen Verhaltensweisen, die vom W3C zugelassen sind und die für die [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]-Implementierung der <xref:System.Xml.Xsl.XslTransform>-Klasse implementiert sind, sowie jeweils den Abschnitt der W3C-Empfehlung zu XSLT 1.0, in der das entsprechende Problem behandelt wird.  
  
|Problem|Verhalten|Bereich|  
|-------------|--------------|-------------|  
|Ein Textknoten entspricht sowohl `xsl:strip-space` als auch `xsl:preserve-space`.|Wiederherstellen|3.4|  
|Ein Quellknoten entspricht mehreren Vorlagenregeln.|Wiederherstellen|5.5|  
|Ein Namespace-URI (Uniform Resource Identifier) ist als Alias für mehrere Namespace-URIs deklariert, die alle die gleiche Importpriorität haben.|Wiederherstellen|7.1.1|  
|Das Namensattribut in `xsl:attribute` und `xsl:element`, das aus einer Attributwertvorlage generiert wurde, ist kein gültiger qualifizierter Name (QName).|Ausgelöste Ausnahme|7.1.2 und 7.1.3|  
|Hinzufügen eines Attributs zu einem Element, nachdem dem Elementknoten untergeordnete Knoten hinzugefügt wurden.|Wiederherstellen|7.1.3|  
|Hinzufügen eines Attributs zu beliebiegen Dokumentbestandteilen außer einem Elementknoten.|Wiederherstellen|7.1.3|  
|Instanziierung des Inhalts des `xsl:attribute`-Elements ist kein Textknoten.|Wiederherstellen|7.1.3|  
|Zwei Attributgruppen besitzen dieselbe Importpriorität und denselben erweiterten Namen. Beide verfügen über dieselben Attribute, und es existiert keine weitere Attributgruppe, die das gemeinsame Attribut mit demselben Namen und höherer Importpriorität enthält.|Wiederherstellen|7.1.4|  
|Das `xsl:processing-instruction`-Namesattribut weist keinen NCNamen (Non-Colon Name) und kein Ziel für Verarbeitungsanweisungen auf.|Wiederherstellen|7.3|  
|Bei der Instanziierung des Inhalts von `xsl:processing-instruction` werden statt Textknoten andere Knoten erstellt.|Wiederherstellen|7.3|  
|Ergebnisse der Instanziierung des Inhalts von `xsl:processing-instruction` enthalten die Zeichenfolge "`?>`".|Wiederherstellen|7.3|  
|Ergebnisse der Instanziierung des Inhalts von `xsl:comment` enthalten die Zeichenfolge „--“ oder enden mit „-“.|Wiederherstellen|7.4|  
|Bei den Ergebnissen der Instanziierung des Inhalts von `xsl:comment` werden statt Textknoten andere Knoten erstellt.|Wiederherstellen|7.4|  
|Von der Vorlage innerhalb eines Variablenbindungselements wird ein Attributknoten oder ein Namespace-Knoten zurückgegeben.|Wiederherstellen|11.2|  
|Fehler beim Abrufen der Ressource aus dem URI, der in die Dokumentfunktion übergeben wird.|Ausgelöste Ausnahme|12.1|  
|Der URI-Verweis in der Dokumentfunktion enthält einen Fragmentbezeichner, und es tritt ein Fehler bei der Verarbeitung des Fragmentbezeichners auf.|Ausgelöste Ausnahme|12.1|  
|Es sind mehrere Attribute mit demselben Namen vorhanden, die in `cdata-section-elements` nicht als `xls:output` benannt sind, und diese Attribute besitzen dieselbe Importpriorität.|Wiederherstellen|16|  
|Der Prozessor unterstützt den Zeichencodierungswert nicht, der im `encoding`-Attribut des `xsl:output`-Elements angegeben wird.|Wiederherstellen|16.1|  
|`disable-output-escaping` wird für einen Textknoten verwendet, und der Textknoten wird zur Erstellung von Dokumentbestandteilen (außer einem Textknoten) in der Ergebnisstruktur verwendet.|Das `disable-output-escaping`-Attribut wird ignoriert.|16.4|  
|Konvertieren eines Ergebnisstrukturfragments in eine Zahl oder eine Zeichenfolge, falls das Ergebnisstrukturfragment einen Textknoten mit aktiviertem Ausgabeschutz enthält.|Ignoriert|16.4|  
|Der Ausgabeschutz wird für Zeichen deaktiviert, die in der Codierung, die der XSLT-Prozessor für die Ausgabe verwendet, nicht dargestellt werden können.|Ignoriert|16.4|  
|Hinzufügen eines Namespace-Knotens zu einem Element, nachdem diesem entweder untergeordnete Elemente oder Attribute hinzugefügt worden sind.|Wiederherstellen|Errata e25|  
|`xsl:number` ist NaN (keine Zahl), unbegrenzt oder kleiner als 0,5.|Wiederherstellen|Errata e24|  
|Das zweite node-set-Argument der Dokumentfunktion ist leer, und der URI-Verweis ist relativ|Wiederherstellen|Errata e14|  
  
 Die Abschnitte aus den Errata finden Sie im W3C-Dokument "XSL Transformations (XSLT) Version 1.0 Specification Errata" unter www.w3.org/1999/11/REC-xslt-19991116-errata (nur auf Englisch verfügbar).  
  
## <a name="custom-defined-implementation-behaviors"></a>Benutzerdefiniertes Implementierungsverhalten  
 Bestimmte Verhaltensweisen sind einzigartig für die Implementierung der <xref:System.Xml.Xsl.XslTransform>-Klasse. In diesem Abschnitt werden die anbieterspezifischen Implementierungen von `xsl:sort` und die optionalen Funktionen erläutert, die von der <xref:System.Xml.Xsl.XslTransform>-Klasse unterstützt werden.  
  
## <a name="xslsort"></a>xsl:sort  
 In Bezug auf die Verwendung einer Transformation für eine Sortierung werden in der W3C-Empfehlung zu XSLT 1.0 einige Beobachtungen beschrieben. Dies sind:  
  
-   Zwei XSLT-Prozessoren können konforme Prozessoren sein, aber dennoch eine unterschiedliche Sortierung durchführen.  
  
-   Nicht alle XSLT-Prozessoren unterstützen die gleichen Sprachen.  
  
-   Unterschiedliche Prozessoren können für eine bestimmte Sprache unterschiedliche Sortierungen durchführen, die nicht in `xsl:sort.` angegeben sind.  
  
 In der folgenden Tabelle wird das Sortierverhalten dargestellt, das für die einzelnen Datentypen in der .NET Framework-Implementierung einer Transformation mit der <xref:System.Xml.Xsl.XslTransform>-Klasse implementiert ist.  
  
|Datentyp|Sortierverhalten|  
|---------------|----------------------|  
|Text|Daten werden mithilfe der String.Compare-Methode der Common Language Runtime (CLR) und des betreffenden Gebietsschemas sortiert. Wenn der Datentyp Text<xref:System.Xml.Xsl.XslTransform> ist, ist das Sortierverhalten in der -Klasse mit dem Verhalten des Zeichenfolgenvergleichs der CLR identisch.|  
|Anzahl|Numerische Werte werden als Zahlen der XML Path Language (XPath) behandelt und gemäß der Richtlinien in der W3C-Empfehlung zu XML Path Languages (XPath), Version 1.0, Abschnitt 3.5 (www.w3.org/TR/xpath.html#numbers), sortiert.|  
  
## <a name="optional-features-supported"></a>Unterstützte optionale Funktionen  
 In der folgenden Tabelle sind die Funktionen aufgeführt, die ein XSLT-Prozessor optional implementieren kann und die in der <xref:System.Xml.Xsl.XslTransform>-Klasse implementiert sind.  
  
|Funktion|Referenzdokumentation|Hinweise|  
|-------------|------------------------|-----------|  
|Das `disable-output-escaping`-Attribut für das `<xsl:text...>`-Tag und das `<xsl:value-of...>`-Tag.|W3C-Empfehlung zu XSLT 1.0,<br /><br /> Abschnitt 16.4|Das `disable-output-escaping`-Attribut wird ignoriert, wenn das `xsl:text`-Element oder das `xsl:value-of`-Element in einem `xsl:comment`-Element, einem `xsl:processing-instruction`-Element oder einem `xsl:attribute`-Element verwendet wird.<br /><br /> Ergebnisstrukturfragmente, die Text enthalten, und deren Textausgabe nicht geschützt wurde, werden nicht unterstützt.<br /><br /> Das disable-output-escaping<xref:System.Xml.XmlReader>-Attribut wird bei der Transformation in ein <xref:System.Xml.XmlWriter>-Objekt oder ein -Objekt ignoriert.|  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.Xml.Xsl.XslTransform>  
 [Implementierung des XSLT-Prozessors durch die XslTransform-Klasse](../../../../docs/standard/data/xml/xsltransform-class-implements-the-xslt-processor.md)  
 [XSLT-Transformationen mit der XslTransform-Klasse](../../../../docs/standard/data/xml/xslt-transformations-with-the-xsltransform-class.md)  
 [„XPathNavigator“ in Transformationen](../../../../docs/standard/data/xml/xpathnavigator-in-transformations.md)  
 [„XPathNodeIterator“ in Transformationen](../../../../docs/standard/data/xml/xpathnodeiterator-in-transformations.md)  
 [XPathDocument-Eingaben in XslTransform](../../../../docs/standard/data/xml/xpathdocument-input-to-xsltransform.md)  
 [XmlDataDocument-Eingaben in „XslTransform“](../../../../docs/standard/data/xml/xmldatadocument-input-to-xsltransform.md)  
 [XmlDocument-Eingaben in „XslTransform“](../../../../docs/standard/data/xml/xmldocument-input-to-xsltransform.md)
