---
title: Übersicht über die SoundPlayer-Klasse
ms.date: 03/30/2017
helpviewer_keywords:
- playing sounds [Windows Forms], SoundPlayer class
- SoundPlayer class [Windows Forms], about SoundPlayer class
- sounds [Windows Forms], playing
ms.assetid: fcebb938-62b9-4677-9cbe-6465bc863e22
ms.openlocfilehash: 31ce87303b7b96cfd14d4daf07fd21c9de91a548
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="soundplayer-class-overview"></a>Übersicht über die SoundPlayer-Klasse
Die <xref:System.Media.SoundPlayer>-Klasse ermöglicht es Ihnen, Sounds problemlos in Ihre Anwendungen zu integrieren.  
  
 Die <xref:System.Media.SoundPlayer> Klasse Audiodateien im WAV-Format aus einer Ressource oder UNC-Namen oder HTTP-Speicherorte wiedergeben kann. Darüber hinaus die <xref:System.Media.SoundPlayer> -Klasse ermöglicht es Ihnen zu laden oder Wiedergeben von Sounds asynchron.  
  
 Sie können auch die <xref:System.Media.SystemSounds>-Klasse verwenden, um allgemeine Systemsounds wiederzugeben, einschließlich eines akustischen Signals.  
  
## <a name="commonly-used-properties-methods-and-events"></a>Häufig verwendete Eigenschaften, Methoden und Ereignisse  
  
|Name|Beschreibung|  
|----------|-----------------|  
|<xref:System.Media.SoundPlayer.SoundLocation%2A>-Eigenschaft|Der Dateipfad oder die Webadresse des Sounds. Zulässige Werte sind UNC oder HTTP.|  
|<xref:System.Media.SoundPlayer.LoadTimeout%2A>-Eigenschaft|Die Anzahl an Millisekunden, die das Programm wartet, um einen Sound zu laden, bevor es eine Ausnahme auslöst. Der Standardwert ist 10 Sekunden.|  
|<xref:System.Media.SoundPlayer.IsLoadCompleted%2A>-Eigenschaft|Ein boolescher Wert, der angibt, ob der Sound fertig geladen wurde.|  
|<xref:System.Media.SoundPlayer.Load%2A>-Methode|Lädt einen Sound synchron.|  
|<xref:System.Media.SoundPlayer.LoadAsync%2A>-Methode|Fängt an, einen Sound asynchron zu laden. Wenn der Ladevorgang abgeschlossen ist, löst die <xref:System.Media.SoundPlayer.OnLoadCompleted%2A> Ereignis.|  
|<xref:System.Media.SoundPlayer.Play%2A>-Methode|Gibt den Sound angegeben wird, der <xref:System.Media.SoundPlayer.SoundLocation%2A> oder <xref:System.Media.SoundPlayer.Stream%2A> Eigenschaft in einem neuen Thread.|  
|<xref:System.Media.SoundPlayer.PlaySync%2A>-Methode|Gibt den Sound angegeben wird, der <xref:System.Media.SoundPlayer.SoundLocation%2A> oder <xref:System.Media.SoundPlayer.Stream%2A> Eigenschaft im aktuellen Thread.|  
|<xref:System.Media.SoundPlayer.Stop%2A>-Methode|Beendet den aktuell wiedergegebenen Sound.|  
|<xref:System.Media.SoundPlayer.LoadCompleted>-Ereignis|Wird ausgelöst, nachdem versucht wurde, einen Sound zu laden.|  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.Media.SoundPlayer>  
 <xref:System.Media.SystemSounds>
