---
title: 'Vorgehensweise: Exportieren von benutzerdefinierten Richtlinienassertionen'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 99030386-43b0-4f7b-866d-17ea307f5cbd
ms.openlocfilehash: 4182007d32ea857aa333542b4df29da18b8062df
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="how-to-export-custom-policy-assertions"></a>Vorgehensweise: Exportieren von benutzerdefinierten Richtlinienassertionen
Richtlinienassertionen beschreiben die Funktionen und Anforderungen eines Dienstendpunkts. Dienstanwendungen können benutzerdefinierte Richtlinienassertionen in Dienstmetadaten verwenden, um Endpunkt-, Bindungs- oder Vertragsanpassungsinformationen an die Clientanwendung zu übermitteln. Windows Communication Foundation (WCF) können um Assertionen in Richtlinienausdrücke in WSDL-Bindungen auf den Endpunkt, den Vorgang oder Nachrichtenbetreffs, abhängig von den Funktionen oder Anforderungen, kommunizieren, zu exportieren.  
  
 Exportieren Sie benutzerdefinierte Richtlinienassertionen, indem Sie die <xref:System.ServiceModel.Description.IPolicyExportExtension?displayProperty=nameWithType>-Schnittstelle für <xref:System.ServiceModel.Channels.BindingElement?displayProperty=nameWithType> implementieren und das Bindungselement entweder direkt in die Bindung des Dienstendpunkts einfügen oder das Bindungselement in der Anwendungskonfigurationsdatei registrieren. Bei der Implementierung des Richtlinienexports sollte die benutzerdefinierte Richtlinienassertion der entsprechenden <xref:System.Xml.XmlElement?displayProperty=nameWithType> zum <xref:System.ServiceModel.Description.PolicyAssertionCollection?displayProperty=nameWithType>, der in der <xref:System.ServiceModel.Description.PolicyConversionContext?displayProperty=nameWithType>-Methode übergeben wird, als <xref:System.ServiceModel.Description.IPolicyExportExtension.ExportPolicy%2A>-Instanz hinzugefügt werden.  
  
 Außerdem müssen Sie die <xref:System.ServiceModel.Description.MetadataExporter.PolicyVersion%2A>-Eigenschaft der <xref:System.ServiceModel.Description.WsdlExporter>-Klasse überprüfen und geschachtelte Richtlinienausdrücke und Attribute des Richtlinienframework anhand der angegebenen Richtlinienversion in den richtigen Namespace exportieren.  
  
 Um benutzerdefinierte Richtlinienassertionen zu importieren, finden Sie unter <xref:System.ServiceModel.Description.IPolicyImportExtension?displayProperty=nameWithType> und [Vorgehensweise: Importieren von benutzerdefinierten Richtlinienassertionen](../../../../docs/framework/wcf/extending/how-to-import-custom-policy-assertions.md).  
  
### <a name="to-export-custom-policy-assertions"></a>So exportieren Sie benutzerdefinierte Richtlinienassertionen  
  
1.  Implementieren Sie die <xref:System.ServiceModel.Description.IPolicyExportExtension?displayProperty=nameWithType>-Schnittstelle für <xref:System.ServiceModel.Channels.BindingElement?displayProperty=nameWithType>. Im folgenden Codebeispiel wird die Implementierung einer benutzerdefinierten Richtlinienassertion auf der Bindungsebene veranschaulicht.  
  
     [!code-csharp[CustomPolicySample#14](../../../../samples/snippets/csharp/VS_Snippets_CFX/custompolicysample/cs/policyexporter.cs#14)]
     [!code-vb[CustomPolicySample#14](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/custompolicysample/vb/policyexporter.vb#14)]  
  
2.  Fügen Sie das Bindungselement programmgesteuert oder mithilfe einer Anwendungskonfigurationsdatei in die Endpunktbindung ein. Anweisungen hierzu finden Sie in den folgenden Verfahren.  
  
### <a name="to-insert-a-binding-element-using-an-application-configuration-file"></a>So fügen Sie ein Bindungselement mit einer Anwendungskonfigurationsdatei ein  
  
1.  Implementieren Sie <xref:System.ServiceModel.Configuration.BindingElementExtensionElement?displayProperty=nameWithType> für das Bindungselement der benutzerdefinierten Richtlinienassertion.  
  
2.  Fügen Sie die bindungselementerweiterung auf die Konfigurationsdatei mit den [ \<BindingElementExtensions >](../../../../docs/framework/configure-apps/file-schema/wcf/bindingelementextensions.md) Element.  
  
3.  Erstellen Sie mit <xref:System.ServiceModel.Channels.CustomBinding?displayProperty=nameWithType> eine benutzerdefinierte Bindung.  
  
### <a name="to-insert-a-binding-element-programmatically"></a>So fügen Sie ein Bindungselement programmgesteuert ein  
  
1.  Erstellen Sie ein neues <xref:System.ServiceModel.Channels.BindingElement?displayProperty=nameWithType>, und fügen Sie es <xref:System.ServiceModel.Channels.CustomBinding?displayProperty=nameWithType> hinzu.  
  
2.  Fügen Sie die benutzerdefinierte Bindung aus Schritt 1 einem neuen Endpunkt hinzu, und fügen Sie diesen neuen Dienstendpunkt <xref:System.ServiceModel.ServiceHost?displayProperty=nameWithType> hinzu, indem Sie die <xref:System.ServiceModel.ServiceHost.AddServiceEndpoint%2A>-Methode aufrufen.  
  
3.  Öffnen Sie <xref:System.ServiceModel.ServiceHost>. Im folgenden Codebeispiel wird das Erstellen einer benutzerdefinierten Bindung und das programmgesteuerte Einfügen von Bindungselementen veranschaulicht.  
  
     [!code-csharp[s_imperative#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_imperative/cs/service.cs#1)]
     [!code-vb[s_imperative#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_imperative/vb/service.vb#1)]  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.ServiceModel.Description.IPolicyImportExtension>  
 <xref:System.ServiceModel.Description.IPolicyExportExtension>  
 [Vorgehensweise: Importieren von benutzerdefinierten Richtlinienassertionen](../../../../docs/framework/wcf/extending/how-to-import-custom-policy-assertions.md)
