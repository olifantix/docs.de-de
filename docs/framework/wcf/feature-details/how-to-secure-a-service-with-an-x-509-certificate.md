---
title: "Vorgehensweise: Sichern eines Diensts mit einem X.509-Zertifikat | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2d06c2aa-d0d7-4e5e-ad7e-77416aa1c10b
caps.latest.revision: 8
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 8
---
# Vorgehensweise: Sichern eines Diensts mit einem X.509-Zertifikat
Die Sicherung eines Diensts mithilfe eines X.509\-Zertifikats ist eine grundlegende Technik, die von den meisten Bindungen in [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] verwendet wird.Dieses Thema führt durch die Schritte der Konfiguration eines selbst gehosteten Diensts mit einem X.509\-Zertifikat.  
  
 Eine Voraussetzung ist ein gültiges Zertifikat, das zur Authentifizierung des Diensts verwendet werden kann.Das Zertifikat muss von einer vertrauenswürdigen Zertifizierungsstelle zum Server ausgegeben werden.Ist das Zertifikat ungültig, vertrauen die Clients, die versuchen, den Dienst zu verwenden, dem Dienst nicht, und es wird keine Verbindung aufgebaut.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] zur Verwendung von Zertifikaten finden Sie unter [Verwenden von Zertifikaten](../../../../docs/framework/wcf/feature-details/working-with-certificates.md).  
  
### So konfigurieren Sie einen Dienst mit einem Zertifikat mithilfe von Code  
  
1.  Erstellen Sie den Dienstvertrag und den implementierten Dienst.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Entwerfen und Implementieren von Diensten](../../../../docs/framework/wcf/designing-and-implementing-services.md).  
  
2.  Erstellen Sie eine Instanz der <xref:System.ServiceModel.WSHttpBinding>\-Klasse, und legen Sie deren Sicherheitsmodus auf <xref:System.ServiceModel.SecurityMode> fest. Dies wird im folgenden Code veranschaulicht.  
  
     [!code-csharp[C_SecureWithCertificate#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#1)]
     [!code-vb[C_SecureWithCertificate#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#1)]  
  
3.  Erstellen Sie zwei <xref:System.Type>\-Variablen, je eine für den Vertragstyp und den implementierten Vertrag. Dies wird im folgenden Code veranschaulicht.  
  
     [!code-csharp[C_SecureWithCertificate#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#2)]
     [!code-vb[C_SecureWithCertificate#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#2)]  
  
4.  Erstellen Sie eine Instanz der <xref:System.Uri>\-Klasse für die Basisadresse des Diensts.Da `WSHttpBinding` den HTTP\-Transport nutzt, muss der Uniform Resource Identifier \(URI\) mit einem Schema beginnen. Andernfalls löst [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] eine Ausnahme aus, wenn der Dienst geöffnet wird.  
  
     [!code-csharp[C_SecureWithCertificate#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#3)]
     [!code-vb[C_SecureWithCertificate#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#3)]  
  
5.  Erstellen Sie eine neue Instanz der <xref:System.ServiceModel.ServiceHost>\-Klasse mit der Variablen des implementierten Vertragstyps und dem URI.  
  
     [!code-csharp[C_SecureWithCertificate#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#4)]
     [!code-vb[C_SecureWithCertificate#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#4)]  
  
6.  Fügen Sie einen <xref:System.ServiceModel.Description.ServiceEndpoint> zum Dienst hinzu, indem Sie die <xref:System.ServiceModel.ServiceHost.AddServiceEndpoint%2A>\-Methode verwenden.Übergeben Sie den Vertrag, die Bindung und eine Endpunktadresse an den Konstruktor. Dies wird im folgenden Code veranschaulicht.  
  
     [!code-csharp[C_SecureWithCertificate#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#5)]
     [!code-vb[C_SecureWithCertificate#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#5)]  
  
7.  Optional.Um Metadaten vom Dienst abzufragen, erstellen Sie ein neues <xref:System.ServiceModel.Description.ServiceMetadataBehavior>\-Objekt und legen Sie die <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpGetEnabled%2A>\-Eigenschaft auf `true` fest.  
  
     [!code-csharp[C_SecureWithCertificate#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#6)]
     [!code-vb[C_SecureWithCertificate#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#6)]  
  
8.  Verwenden Sie die <xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential.SetCertificate%2A>\-Methode der <xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential>\-Klasse, um das gültige Zertifikat zum Dienst hinzuzufügen.Die Methode kann eine von diversen Methoden nutzen, um ein Zertifikat zu suchen.In diesem Beispiel wird die <xref:System.Security.Cryptography.X509Certificates.X509FindType>\-Enumeration verwendet.Die Enumeration gibt an, dass der gelieferte Wert der Name der Entität ist, an die das Zertifikat herausgegeben wurde.  
  
     [!code-csharp[C_SecureWithCertificate#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#7)]
     [!code-vb[C_SecureWithCertificate#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#7)]  
  
9. Rufen Sie die <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A>\-Methode auf, um die Dienstüberwachung zu starten.Sollten Sie eine Konsolenanwendung erstellen, rufen Sie die <xref:System.Console.ReadLine%2A>\-Methode auf, um den Dienst im Überwachungsstatus zu halten.  
  
     [!code-csharp[C_SecureWithCertificate#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#8)]
     [!code-vb[C_SecureWithCertificate#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#8)]  
  
## Beispiel  
 Im folgenden Beispiel wird die <xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential.SetCertificate%2A>\-Methode verwendet, um einen Dienst mit einem X.509\-Zertifikat zu konfigurieren.  
  
 [!code-csharp[C_SecureWithCertificate#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#9)]
 [!code-vb[C_SecureWithCertificate#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#9)]  
  
## Kompilieren des Codes  
 Die folgenden Namespaces sind zum Kompilieren des Codes erforderlich:  
  
-   <xref:System>  
  
-   <xref:System.ServiceModel>  
  
-   <xref:System.ServiceModel.Channels>  
  
-   <xref:System.Web.Services.Description>  
  
-   <xref:System.Security.Cryptography.X509Certificates>  
  
-   <xref:System.Runtime.Serialization>  
  
## Siehe auch  
 [Verwenden von Zertifikaten](../../../../docs/framework/wcf/feature-details/working-with-certificates.md)