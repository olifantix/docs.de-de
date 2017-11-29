---
title: "&lt;SectionGroup&gt; -Element für &lt;\"configSections\"&gt;"
ms.date: 05/01/2017
ms.prod: .net-framework
ms.technology: dotnet-clr
ms.topic: article
f1_keywords: http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/configSections/sectionGroup
helpviewer_keywords:
- sectionGroup Element
- <sectionGroup> Element
ms.assetid: 6c27f9e2-809c-4bc9-aca9-72f90360e7a3
author: guardrex
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: 5c5c040a322c38da319f2e964519f94d761327e0
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/18/2017
---
# <a name="sectiongroup-element-for-configsections"></a><span data-ttu-id="9b1ca-102">\<SectionGroup >-Element für \<ConfigSections ></span><span class="sxs-lookup"><span data-stu-id="9b1ca-102">\<sectionGroup> element for \<configSections></span></span>

<span data-ttu-id="9b1ca-103">Definiert einen Namespace für Konfigurationsabschnitte.</span><span class="sxs-lookup"><span data-stu-id="9b1ca-103">Defines a namespace for configuration sections.</span></span>

<span data-ttu-id="9b1ca-104">[**\<configuration>**](~/docs/framework/configure-apps/file-schema/configuration-element.md) </span><span class="sxs-lookup"><span data-stu-id="9b1ca-104">[**\<configuration>**](~/docs/framework/configure-apps/file-schema/configuration-element.md) </span></span>  
<span data-ttu-id="9b1ca-105">&nbsp;&nbsp;[**\<ConfigSections >**](~/docs/framework/configure-apps/file-schema/configsections-element-for-configuration.md) </span><span class="sxs-lookup"><span data-stu-id="9b1ca-105">&nbsp;&nbsp;[**\<configSections>**](~/docs/framework/configure-apps/file-schema/configsections-element-for-configuration.md) </span></span>  
<span data-ttu-id="9b1ca-106">&nbsp;&nbsp;&nbsp;&nbsp;**\<SectionGroup >**</span><span class="sxs-lookup"><span data-stu-id="9b1ca-106">&nbsp;&nbsp;&nbsp;&nbsp;**\<sectionGroup>**</span></span>

## <a name="syntax"></a><span data-ttu-id="9b1ca-107">Syntax</span><span class="sxs-lookup"><span data-stu-id="9b1ca-107">Syntax</span></span>

```xml
<sectionGroup name="section group name">
  <!-- Configuration sections -->
</sectionGroup>
```

## <a name="attribute"></a><span data-ttu-id="9b1ca-108">Attribut</span><span class="sxs-lookup"><span data-stu-id="9b1ca-108">Attribute</span></span>

|           | <span data-ttu-id="9b1ca-109">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="9b1ca-109">Description</span></span> |
| --------- | ----------- |
| <span data-ttu-id="9b1ca-110">**name**</span><span class="sxs-lookup"><span data-stu-id="9b1ca-110">**name**</span></span>  | <span data-ttu-id="9b1ca-111">Erforderliches Attribut.</span><span class="sxs-lookup"><span data-stu-id="9b1ca-111">Required attribute.</span></span><br><br><span data-ttu-id="9b1ca-112">Gibt den Namen der Abschnittsgruppe, die Sie definieren.</span><span class="sxs-lookup"><span data-stu-id="9b1ca-112">Specifies the name of the section group you are defining.</span></span> |

## <a name="parent-element"></a><span data-ttu-id="9b1ca-113">Übergeordnetes Element</span><span class="sxs-lookup"><span data-stu-id="9b1ca-113">Parent element</span></span>

|     | <span data-ttu-id="9b1ca-114">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="9b1ca-114">Description</span></span> |
| --- | ----------- |
| [<span data-ttu-id="9b1ca-115">**\<ConfigSections >** Element</span><span class="sxs-lookup"><span data-stu-id="9b1ca-115">**\<configSections>** Element</span></span>](~/docs/framework/configure-apps/file-schema/configsections-element-for-configuration.md) | <span data-ttu-id="9b1ca-116">Enthält die Konfiguration im Abschnitt und Namespacedeklarationen.</span><span class="sxs-lookup"><span data-stu-id="9b1ca-116">Contains configuration section and namespace declarations.</span></span> |

## <a name="child-elements"></a><span data-ttu-id="9b1ca-117">Untergeordnete Elemente</span><span class="sxs-lookup"><span data-stu-id="9b1ca-117">Child elements</span></span>

|     | <span data-ttu-id="9b1ca-118">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="9b1ca-118">Description</span></span> |
| --- | ----------- |
| [<span data-ttu-id="9b1ca-119">**\<Abschnitt >**</span><span class="sxs-lookup"><span data-stu-id="9b1ca-119">**\<section>**</span></span>](~/docs/framework/configure-apps/file-schema/section-element.md) | <span data-ttu-id="9b1ca-120">Enthält eine Deklaration der Konfiguration im Abschnitt.</span><span class="sxs-lookup"><span data-stu-id="9b1ca-120">Contains a configuration section declaration.</span></span> |

## <a name="remarks"></a><span data-ttu-id="9b1ca-121">Hinweise</span><span class="sxs-lookup"><span data-stu-id="9b1ca-121">Remarks</span></span>

<span data-ttu-id="9b1ca-122">Deklarieren eine Abschnittsgruppe erstellt ein Containertag für Konfigurationsabschnitte und stellt sicher, dass keine Namenskonflikte mit Konfigurationsabschnitte, die von einer anderen Person definiert.</span><span class="sxs-lookup"><span data-stu-id="9b1ca-122">Declaring a section group creates a container tag for configuration sections and ensures that there are no naming conflicts with configuration sections defined by someone else.</span></span> <span data-ttu-id="9b1ca-123">Sie können schachteln  **\<SectionGroup >** Elemente in einem anderen.</span><span class="sxs-lookup"><span data-stu-id="9b1ca-123">You can nest **\<sectionGroup>** elements within each other.</span></span>

## <a name="example"></a><span data-ttu-id="9b1ca-124">Beispiel</span><span class="sxs-lookup"><span data-stu-id="9b1ca-124">Example</span></span>

<span data-ttu-id="9b1ca-125">Das folgende Beispiel zeigt, wie zum Deklarieren einer Abschnittsgruppe und Abschnitte innerhalb einer Abschnittsgruppe deklarieren:</span><span class="sxs-lookup"><span data-stu-id="9b1ca-125">The following example shows how to declare a section group and declare sections within a section group:</span></span>

```xml
<configuration>
  <configSections>
    <sectionGroup name="mySectionGroup">
      <section name="mySection"
               type="System.Configuration.NameValueSectionHandler,System" />
    </sectionGroup>
  </configSections>
  <mySectionGroup>
    <mySection>
      <add key="key1" value="value1" />
    </mySection>
  </mySectionGroup>
</configuration>
```

## <a name="configuration-file"></a><span data-ttu-id="9b1ca-126">Konfigurationsdatei</span><span class="sxs-lookup"><span data-stu-id="9b1ca-126">Configuration file</span></span>

<span data-ttu-id="9b1ca-127">Dieses Element kann in der Anwendungskonfigurationsdatei Computerkonfigurationsdatei verwendet werden (*"Machine.config"*), und *"Web.config"* Dateien, die nicht auf Anwendungsebene Verzeichnis sind.</span><span class="sxs-lookup"><span data-stu-id="9b1ca-127">This element can be used in the application configuration file, machine configuration file (*Machine.config*), and *Web.config* files that are not at the application directory level.</span></span>

## <a name="see-also"></a><span data-ttu-id="9b1ca-128">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="9b1ca-128">See also</span></span>

[<span data-ttu-id="9b1ca-129">Konfigurationsdateischema für .NET Framework</span><span class="sxs-lookup"><span data-stu-id="9b1ca-129">Configuration file schema for the .NET Framework</span></span>](~/docs/framework/configure-apps/file-schema/index.md)