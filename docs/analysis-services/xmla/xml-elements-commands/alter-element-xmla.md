---
title: "Alter 元素 (XMLA) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Alter Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Alter
- microsoft.xml.analysis.alter
- urn:schemas-microsoft-com:xml-analysis#Alter
helpviewer_keywords: Alter command
ms.assetid: 84e58385-c9ba-48fa-a867-94d35b777a56
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 08bc085a99dcd6f9059f1dbba4355aca368bd219
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="alter-element-xmla"></a>Alter 元素 (XMLA)
  包含所使用的 Analysis Services 指令碼語言 (ASSL) 元素[Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法來修改物件的執行個體上[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
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
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|子元素|[物件](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)， [ObjectDefinition](../../../analysis-services/xmla/xml-elements-properties/objectdefinition-element-xmla.md)|  
  
## <a name="attributes"></a>屬性  
  
|Attribute|Description|  
|---------------|-----------------|  
|AllowCreate|(選擇性**布林**屬性) 指出物件是否定義在**Alter**應建立命令，如果它們尚不存在。<br /><br /> 如果設定為 true 中, 定義的物件**ObjectDefinition**上所建立的項目[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體如果已經存在。 換句話說， **Alter**命令會被視為**建立**命令如果物件不存在的執行個體上。<br /><br /> 如果這個屬性被省略或設定為**false**，如果物件不存在，就會發生錯誤。|  
|ObjectExpansion|(選擇性**列舉**屬性) 定義的所要執行的更改範圍**Execute**方法。<br /><br /> 如果設定為*ObjectProperties*、 **ObjectDefinition**項目應該包含要改變的主要物件的完整定義包括從屬次要物件。 要更改之物件的從屬主要物件會維持不變。<br /><br /> 附註： 當使用*ObjectProperties*設定[ClrAssembly](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md)資料型別，[資料](../../../analysis-services/scripting/objects/data-element-assl.md)相關聯的項目[ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md)不需要指定資料類型。 如果未指定， **ClrAssembly**會使用現有的檔案。<br /><br /> 如果設定為*ExpandFull*、 **ObjectDefinition**項目應該包含不只是要變更、 物件的定義，但是也就是物件的下階的所有主要物件的定義若要改變。<br /><br /> 注意： *ExpandFull*設定無法搭配[伺服器](../../../analysis-services/scripting/objects/server-element-assl.md)項目。|  
|範圍。|(選擇性**列舉**屬性) 定義中定義之物件的持續時間**ObjectDefinition**項目。<br /><br /> 如果設定為*工作階段*中, 定義的物件**ObjectDefinition**元素只存在於 XMLA 工作階段的持續時間。<br /><br /> 注意： 當使用*工作階段*設定， **ObjectDefinition**元素只能包含[維度](../../../analysis-services/scripting/objects/dimension-element-assl.md)， [Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)，或[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md) ASSL 元素。<br /><br /> 如果省略此屬性，則中定義的物件**ObjectDefinition**項目會保存[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體。|  
  
## <a name="remarks"></a>備註  
 每個**Alter**命令會變更所指定的父物件底下某個主要物件的定義[ParentObject](../../../analysis-services/xmla/xml-elements-properties/parentobject-element-xmla.md)項目。  
  
## <a name="see-also"></a>請參閱＜  
 [命令 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
