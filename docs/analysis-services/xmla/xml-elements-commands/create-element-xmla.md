---
title: "Create 元素 (XMLA) |Microsoft 文件"
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
apiname:
- Create Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Create
- urn:schemas-microsoft-com:xml-analysis#Create
- microsoft.xml.analysis.create
helpviewer_keywords:
- Create command (XMLA)
ms.assetid: a623d362-a1ac-40e4-8816-65fac89cb391
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a5420a85c65a29a09da519207206d3406c4cd384
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="create-element-xmla"></a>Create 元素 (XMLA)
  包含所使用的 Analysis Services 指令碼語言 (ASSL) 元素**Execute**上建立物件的方法[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Command>  
   <Create Scope="enum" AllowOverwrite="boolean">  
      <ParentObject>...</ParentObject>  
      <ObjectDefinition>...</ObjectDefinition>  
   </Create>  
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
|子元素|[ObjectDefinition](../../../analysis-services/xmla/xml-elements-properties/objectdefinition-element-xmla.md)， [ParentObject](../../../analysis-services/xmla/xml-elements-properties/parentobject-element-xmla.md)|  
  
## <a name="attributes"></a>屬性  
  
|Attribute|Description|  
|---------------|-----------------|  
|AllowOverwrite|選擇性 **Boolean** 屬性。 如果設為 True 中, 定義的物件**ObjectDefinition**項目可以覆寫現有物件上[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體。 如果這個屬性被省略或設定為 False，現有物件的存在就會產生錯誤。|  
|範圍。|選擇性**列舉**屬性。 定義中定義之物件的持續時間**ObjectDefinition**項目。 如果省略此屬性，則中定義的物件**ObjectDefinition**項目會保存[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體。 有下列值：<br /><br /> *工作階段*： 中定義的物件**ObjectDefinition**元素只存在於 XML for Analysis (XMLA) 工作階段持續時間。<br />                  請注意，當使用*工作階段*設定， **ObjectDefinition**元素只能包含[維度](../../../analysis-services/scripting/objects/dimension-element-assl.md)， [Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)，或[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md) ASSL 元素。|  
  
## <a name="remarks"></a>備註  
 每個**建立**作業會建立提供的父系底下某個主要物件**ParentObject**項目。 如果您了省略父物件，它就會被假設為目的地 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體。 如果主要物件的父系不是目的地執行個體，這樣做就會產生錯誤。  
  
## <a name="example"></a>範例  
 下列範例會建立名為的空白資料庫**測試資料庫**上[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體。  
  
```  
  
      <Create xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
   <ObjectDefinition>  
      <Database xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
         <Name>Test Database</Name>  
         <Description>A test database.</Description>  
      </Database>  
   </ObjectDefinition>  
</Create>  
```  
  
## <a name="see-also"></a>另請參閱  
 [命令 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  

