---
title: 定義和識別物件（XMLA） |Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62727541"
---
# <a name="defining-and-identifying-objects-xmla"></a>定義和識別物件 (XMLA)
  透過使用物件識別碼與物件參考，在 XML for Analysis (XMLA) 命令中識別物件，並使用 Analysis Services 指令碼語言 (ASSL) 元素 XMLA 命令來定義。  
  
## <a name="object-identifiers"></a>物件識別碼  
 物件的識別方式是使用實例[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]上所定義之物件的唯一識別碼。 當 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 建立物件時，可以明確指定或是由 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體決定物件識別碼。 您可以使用[探索](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover)方法來抓取後續`Discover`或[執行](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute)方法呼叫的物件識別碼。  
  
## <a name="object-references"></a>物件參考  
 有數個 XMLA 命令，例如[Delete](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/delete-element-xmla)或[Process](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla)，會使用物件參考，以明確的方式來參考物件。 物件參考包含命令執行所在之物件的物件識別碼和該物件之上階的物件識別碼。 例如，資料分割的物件參考包含資料分割的物件識別碼，以及該資料分割的父量值群組、Cube 及資料庫之物件識別碼。  
  
## <a name="object-definitions"></a>物件定義  
 XMLA 中的[create](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla)和[alter](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla)命令會分別建立或更改[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]實例上的物件。 這些物件的定義會以包含 ASSL 元素的[ObjectDefinition](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/objectdefinition-element-xmla)元素表示。 您可以使用[ID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla)元素，為所有主要和許多次要物件明確指定物件識別碼。 如果未使用 `ID` 元素，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體會使用待識別物件的命名慣例來提供唯一識別碼。 如需如何使用`Create`和`Alter`命令來定義物件的詳細資訊，請參閱[建立和改變物件 &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects)。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;XMLA&#41;的物件元素](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)   
 [&#40;XMLA&#41;的 ParentObject 元素](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)   
 [&#40;XMLA&#41;的 Source 元素](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/source-element-xmla)   
 [&#40;XMLA&#41;的目標元素](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/target-element-xmla)   
 [在 Analysis Services 中使用 XMLA 進行開發](developing-with-xmla-in-analysis-services.md)  
  
  
