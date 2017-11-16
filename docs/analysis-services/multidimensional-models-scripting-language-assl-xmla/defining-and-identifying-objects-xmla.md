---
title: "定義和識別物件 (XMLA) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- objects [XML for Analysis]
- identifying objects [XML for Analysis]
- XML for Analysis, objects
- object references [XML for Analysis]
- object identifiers [XML for Analysis]
- object definitions [XML for Analysis]
- XMLA, objects
ms.assetid: 43b65f6d-0123-4556-81f0-c7a0b84361e5
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 136679f6596d7e0bf3c33eca51461af13a9fa6d0
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="defining-and-identifying-objects-xmla"></a>定義和識別物件 (XMLA)
  透過使用物件識別碼與物件參考，在 XML for Analysis (XMLA) 命令中識別物件，並使用 Analysis Services 指令碼語言 (ASSL) 元素 XMLA 命令來定義。  
  
## <a name="object-identifiers"></a>物件識別碼  
 所使用的執行個體上所定義之物件的唯一識別碼可識別物件[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。 當 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 建立物件時，可以明確指定或是由 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體決定物件識別碼。 您可以使用[探索](../../analysis-services/xmla/xml-elements-methods-discover.md)方法來擷取物件識別碼，以後續**探索**或[Execute](../../analysis-services/xmla/xml-elements-methods-execute.md)方法呼叫。  
  
## <a name="object-references"></a>物件參考  
 數個 XMLA 命令，例如[刪除](../../analysis-services/xmla/xml-elements-commands/delete-element-xmla.md)或[程序](../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)，來參考物件以模稜兩可的方式使用物件參考。 物件參考包含命令執行所在之物件的物件識別碼和該物件之上階的物件識別碼。 例如，資料分割的物件參考包含資料分割的物件識別碼，以及該資料分割的父量值群組、Cube 及資料庫之物件識別碼。  
  
## <a name="object-definitions"></a>物件定義  
 [建立](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)和[Alter](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)中 XMLA 命令建立或更改，分別物件上[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體。 這些物件的定義由[ObjectDefinition](../../analysis-services/xmla/xml-elements-properties/objectdefinition-element-xmla.md)包含 assl 元素的元素。 物件識別碼可以明確地指定所有主要和許多次要物件使用[識別碼](../../analysis-services/xmla/xml-elements-properties/id-element-xmla.md)項目。 如果**識別碼**未使用項目，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體會提供唯一的識別碼，取決於用來識別物件命名慣例。 如需有關如何使用**建立**和**Alter**命令來定義物件，請參閱[建立和改變物件 &#40;XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/creating-and-altering-objects-xmla.md).  
  
## <a name="see-also"></a>另請參閱  
 [Object 元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)   
 [ParentObject 元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-properties/parentobject-element-xmla.md)   
 [Source 元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md)   
 [目標項目 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-properties/target-element-xmla.md)   
 [使用 Analysis Services 中的 XMLA 進行開發](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  

