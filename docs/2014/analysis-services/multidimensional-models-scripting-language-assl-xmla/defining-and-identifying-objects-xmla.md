---
title: 定義和識別物件 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- objects [XML for Analysis]
- identifying objects [XML for Analysis]
- XML for Analysis, objects
- object references [XML for Analysis]
- object identifiers [XML for Analysis]
- object definitions [XML for Analysis]
- XMLA, objects
ms.assetid: 43b65f6d-0123-4556-81f0-c7a0b84361e5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ad6c8de47577eccd7797517c8080957d7afe1abd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62727541"
---
# <a name="defining-and-identifying-objects-xmla"></a>定義和識別物件 (XMLA)
  透過使用物件識別碼與物件參考，在 XML for Analysis (XMLA) 命令中識別物件，並使用 Analysis Services 指令碼語言 (ASSL) 元素 XMLA 命令來定義。  
  
## <a name="object-identifiers"></a>物件識別碼  
 使用的執行個體上定義之物件的唯一識別碼可識別物件[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。 當 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 建立物件時，可以明確指定或是由 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體決定物件識別碼。 您可以使用[Discover](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover)方法來擷取物件識別碼，以後續`Discover`或是[Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute)方法呼叫。  
  
## <a name="object-references"></a>物件參考  
 數個 XMLA 命令，例如[刪除](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/delete-element-xmla)或是[程序](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla)，使用物件參考，以指向的物件，以明確的方式。 物件參考包含命令執行所在之物件的物件識別碼和該物件之上階的物件識別碼。 例如，資料分割的物件參考包含資料分割的物件識別碼，以及該資料分割的父量值群組、Cube 及資料庫之物件識別碼。  
  
## <a name="object-definitions"></a>物件定義  
 [Create](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla)並[Alter](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla)中 XMLA 命令建立或更改，分別物件上[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體。 這些物件的定義由[ObjectDefinition](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/objectdefinition-element-xmla)包含 ASSL 元素的項目。 物件可以明確指定識別碼的所有主要物件和許多次要物件使用[識別碼](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla)項目。 如果未使用 `ID` 元素，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體會使用待識別物件的命名慣例來提供唯一識別碼。 如需有關如何使用`Create`並`Alter`命令來定義物件，請參閱[建立和改變物件&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects)。  
  
## <a name="see-also"></a>另請參閱  
 [物件項目&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)   
 [ParentObject 元素&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)   
 [Source 元素&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/source-element-xmla)   
 [Target 項目&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/target-element-xmla)   
 [在 Analysis Services 中使用 XMLA 進行開發](developing-with-xmla-in-analysis-services.md)  
  
  
