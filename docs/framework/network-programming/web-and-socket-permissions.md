---
title: Web- und Socketberechtigungen
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Networking
- positions [.NET Framework], accepting
- sockets, permissions
- network, permissions
- Internet, permissions
- Network Resources
- SocketPermission class, about SocketPermission class
- positions [.NET Framework], connecting
- WebPermission class, about WebPermission class
- permissions [.NET Framework], sockets
- security [.NET Framework], Internet
- positions [.NET Framework], granting
ms.assetid: d51ad8cb-03ae-4a51-bfcd-cfcf6b98afa9
caps.latest.revision: "9"
author: mcleblanc
ms.author: markl
manager: markl
ms.workload: dotnet
ms.openlocfilehash: b426b5e7e6a9b617311db05670f526fc415d591d
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/22/2017
---
# <a name="web-and-socket-permissions"></a>Web- und Socketberechtigungen
Internetsicherheit für Anwendungen, die den <xref:System.Net>-Namespace verwenden, wird von den <xref:System.Net.WebPermission>- und <xref:System.Net.SocketPermission>-Klassen bereitgestellt. Die **WebPermission**-Klasse steuert das Recht einer Anwendung, Daten aus einem URI abzufragen, oder einen URI für das Internet zu verarbeiten. Die **SocketPermission**-Klasse steuert das Recht einer Anwendung zur Verwendung von <xref:System.Net.Sockets.Socket> für das Annehmen von Daten auf einem lokalen Port oder für das Kontaktieren von Remotegeräten, die ein Transportprotokoll an einer anderen Adresse verwenden, und die auf dem Host, der Portnummer und dem Transportprotokoll des Sockets basieren.  
  
 Welche Berechtigungsklasse Sie verwenden, hängt von Ihrem Anwendungstyp ab. Anwendungen, die <xref:System.Net.WebRequest> und seine Nachfolger verwenden, sollten die **WebPermission**-Klasse verwenden, um Berechtigungen zu verwalten. Anwendungen, die Zugriff auf Socketebene verwenden, sollten die **SocketPermission**-Klasse verwenden, um Berechtigungen zu verwalten.  
  
 **WebPermission** und **SocketPermission** definieren zwei Berechtigungen: Akzeptieren und Verbinden. „Akzeptieren“ gewährt der Anwendung das Recht, eine eingehende Verbindung von einer anderen Partei zu beantworten. „Verbinden“ gewährt der Anwendung das Recht, eine eingehende Verbindung von einer anderen Partei zu initiieren.  
  
 Für **SocketPermission**-Instanzen bedeutet „Akzeptieren“, dass eine Anwendung eingehende Verbindungen auf einer lokalen Transportadresse annehmen kann. „Verbinden“ bedeutet, dass eine Anwendung eine Verbindung zu einer Remotetransportadresse (oder einer lokalen Transportadresse) herstellen kann.  
  
 Für **WebPermission**-Instanzen bedeutet „Akzeptieren“, dass eine Anwendung den von **WebPermission** gesteuerten URI weltweit exportieren kann. „Verbinden“ bedeutet, dass eine Anwendung Zugriff auf diesen URI hat (egal ob Remote oder lokal).  
  
## <a name="see-also"></a>Siehe auch  
 [Sicherheit](../../../docs/standard/security/index.md)  
 [Security in Network Programming (Sicherheit in der Netzwerkprogrammierung)](../../../docs/framework/network-programming/security-in-network-programming.md)
