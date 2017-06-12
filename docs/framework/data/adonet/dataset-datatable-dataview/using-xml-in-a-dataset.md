---
title: "Verwenden von XML in einem DataSet | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 35138159-e199-49ec-baf7-1ec6777e171e
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Verwenden von XML in einem DataSet
Mit ADO.NET können Sie ein <xref:System.Data.DataSet> über einen XML\-Stream oder ein XML\-Dokument füllen.  Die können den XML\-Stream oder das XML\-Dokument verwenden, um das <xref:System.Data.DataSet> mit Daten oder Schemainformationen oder mit beidem zu versorgen.  Die vom XML\-Stream oder vom XML\-Dokument bereitgestellten Daten können mit vorhandenen Daten oder Schemainformationen kombiniert werden, die bereits im <xref:System.Data.DataSet> enthalten sind.  
  
 ADO.NET ermöglicht auch das Erstellen einer XML\-Darstellung eines <xref:System.Data.DataSet> mit oder ohne zugehöriges Schema, damit das <xref:System.Data.DataSet> über HTTP übertragen und von anderen Anwendungen oder XML\-fähigen Plattformen verwendet werden kann.  Bei einer XML\-Darstellung eines <xref:System.Data.DataSet> werden die Daten im XML\-Format geschrieben, und das Schema wird, sofern es sich um ein Inlineschema handelt, mit XSD \(XML Schema Definition Language\) geschrieben.  XML und das XML\-Schema stellen ein komfortables Format zum Übertragen des <xref:System.Data.DataSet>\-Inhalts an und von Remoteclients bereit.  
  
## In diesem Abschnitt  
 [DiffGrams](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/diffgrams.md)  
 Bietet Einzelheiten zum DiffGram, einem XML\-Format, das zum Lesen und Schreiben des Inhalts eines <xref:System.Data.DataSet> verwendet wird.  
  
 [Laden eines DataSet aus XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-a-dataset-from-xml.md)  
 Beschreibt verschiedene Möglichkeiten beim Füllen eines <xref:System.Data.DataSet> mit einem XML\-Dokument.  
  
 [Schreiben von 'DataSet'\-Inhalt als XML\-Daten](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/writing-dataset-contents-as-xml-data.md)  
 Erläutert, wie der Inhalt eines <xref:System.Data.DataSet> als XML\-Daten generiert wird und welche XML\-Formatoptionen verwendet werden können.  
  
 [Laden von DataSet\-Schemainformationen aus XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-dataset-schema-information-from-xml.md)  
 Erläutert die <xref:System.Data.DataSet>\-Methoden, die zum Laden des Schemas eines <xref:System.Data.DataSet> aus einem XML\-Dokument verwendet werden.  
  
 [Schreiben von 'DataSet'\-Schema\-Informationen als XSD](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/writing-dataset-schema-information-as-xsd.md)  
 Erläutert, wie ein XML\-Schema verwendet und aus einem <xref:System.Data.DataSet> generiert wird.  
  
 [Synchronisierung zwischen 'DataSet' und 'XmlDataDocument'](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/dataset-and-xmldatadocument-synchronization.md)  
 Erläutert die Möglichkeiten, die in .NET Framework für den synchronen Zugriff auf relationale und hierarchische Darstellungen eines einzigen Datensatzes zur Verfügung stehen. Darüber hinaus wird gezeigt, wie eine synchrone Beziehung zwischen einem <xref:System.Data.DataSet> und einem <xref:System.Xml.XmlDataDocument> erstellt werden kann.  
  
 [Schachteln von 'DataRelations'](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/nesting-datarelations.md)  
 Erläutert die Bedeutung geschachtelter <xref:System.Data.DataRelation>\-Objekte beim Darstellen des Inhalts eines <xref:System.Data.DataSet> als XML\-Daten und beschreibt deren Erstellung.  
  
 [Ableiten einer relationalen 'DataSet'\-Struktur aus einem XML\-Schema \(XSD\)](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/deriving-dataset-relational-structure-from-xml-schema-xsd.md)  
 Beschreibt die relationale Struktur bzw. das Schema eines <xref:System.Data.DataSet>, das aus einem XML\-Schema erstellt wird.  
  
 [Herleiten der relationalen DataSet\-Struktur aus XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/inferring-dataset-relational-structure-from-xml.md)  
 Beschreibt die resultierende relationale Struktur bzw. das Schema eines <xref:System.Data.DataSet>, das beim Herleiten aus XML\-Elementen erstellt wird.  
  
## Verwandte Abschnitte  
 [Übersicht über ADO.NET](../../../../../docs/framework/data/adonet/ado-net-overview.md)  
 Beschreibt die ADO.NET\-Architektur und \-Komponenten und wie diese dazu verwendet werden, auf vorhandene Datenquellen zuzugreifen sowie Anwendungsdaten zu verwalten.  
  
## Siehe auch  
 [DataSets, DataTables und DataViews](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [ADO.NET Verwaltete Anbieter und DataSet\-Entwicklercenter](http://go.microsoft.com/fwlink/?LinkId=217917)