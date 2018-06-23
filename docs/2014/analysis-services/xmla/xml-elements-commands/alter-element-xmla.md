---
title: Alter 元素 (XMLA) |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Alter Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Alter
- microsoft.xml.analysis.alter
- urn:schemas-microsoft-com:xml-analysis#Alter
helpviewer_keywords:
- Alter command
ms.assetid: 84e58385-c9ba-48fa-a867-94d35b777a56
caps.latest.revision: 14
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 5ea2c3ed3105c66b0c0848138acb5941978dd9bf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36035070"
---
# <a name="alter-element-xmla"></a>Alter 元素 (XMLA)
  包含所使用的 Analysis Services 指令碼語言 (ASSL) 元素[Execute](../xml-elements-methods-execute.md)方法來修改物件的執行個體上[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Command>  
   <Alter Scope="enum" AllowCreate="boolean" ObjectExpansion="enum">  
      <Object>...</Object>  
      <ObjectDefinition>...</ObjectDefinition>  
   </Alter>  
</Command>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Command](../xml-elements-properties/command-element-xmla.md)|  
|子元素|[物件](../xml-elements-properties/object-element-xmla.md)， [ObjectDefinition](../xml-elements-properties/objectdefinition-element-xmla.md)|  
  
## <a name="attributes"></a>屬性  
  
|attribute|描述|  
|---------------|-----------------|  
|AllowCreate|(選擇性 `Boolean` 屬性) 指出是否應該建立 `Alter` 命令中定義的物件 (如果它們原本不存在的話)。<br /><br /> 如果設定為 true，系統就會在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體上建立 `ObjectDefinition` 元素中定義的物件 (如果它們原本不存在的話)。 換言之，如果這些物件原本不存在執行個體上，`Alter` 命令就會被視為 `Create` 命令。<br /><br /> 如果這個屬性被省略或設定為 `false`，當這些物件原本不存在時，就會發生錯誤。|  
|ObjectExpansion|(選擇性 `Enum` 屬性) 定義要由 `Execute` 方法執行的更改範圍。<br /><br /> 如果設定為*ObjectProperties*、`ObjectDefinition`項目應該包含要改變的主要物件的完整定義包括從屬次要物件。 要更改之物件的從屬主要物件會維持不變。 **注意：** 時使用*ObjectProperties*設定[ClrAssembly](../../scripting/data-type/assembly-data-type-assl.md)資料型別，[資料](../../scripting/objects/data-element-assl.md)相關聯的項目[ClrAssemblyFile](../../scripting/data-type/clrassemblyfile-data-type-assl.md)不需要指定資料類型。 如果沒有指定，`ClrAssembly` 就會使用現有檔案。 <br /><br /> 如果設定為*ExpandFull*、`ObjectDefinition`項目應該包含不只是要變更、 物件的定義，但這是要改變的下階物件的所有主要物件的定義。 **注意：** *ExpandFull*設定無法搭配[伺服器](../../scripting/objects/server-element-assl.md)項目。|  
|範圍。|(選擇性 `Enum` 屬性) 定義 `ObjectDefinition` 元素中定義之物件的持續時間。<br /><br /> 如果設定為*工作階段*中, 定義的物件`ObjectDefinition`元素只存在於 XMLA 工作階段的持續時間。 **注意：** 時使用*工作階段*設定，`ObjectDefinition`元素只能包含[維度](../../scripting/objects/dimension-element-assl.md)， [Cube](../../scripting/objects/cube-element-assl.md)，或[MiningModel](../../scripting/objects/miningmodel-element-assl.md) ASSL 元素。 <br /><br /> 如果這屬性被省略，`ObjectDefinition` 元素中定義的物件就會保存在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體上。|  
  
## <a name="remarks"></a>備註  
 每個`Alter`命令會變更所指定的父物件底下某個主要物件的定義[ParentObject](../xml-elements-properties/parentobject-element-xmla.md)項目。  
  
## <a name="see-also"></a>另請參閱  
 [命令&#40;XMLA&#41;](xml-elements-commands.md)  
  
  