---
title: Create 元素 (XMLA) |Microsoft 文件
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
- Create Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Create
- urn:schemas-microsoft-com:xml-analysis#Create
- microsoft.xml.analysis.create
helpviewer_keywords:
- Create command (XMLA)
ms.assetid: a623d362-a1ac-40e4-8816-65fac89cb391
caps.latest.revision: 17
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 19e7673c63d7e305d706efb910222f8ba0da7215
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36136074"
---
# <a name="create-element-xmla"></a>Create 元素 (XMLA)
  包含所使用的 Analysis Services 指令碼語言 (ASSL) 元素`Execute`上建立物件的方法[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體。  
  
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
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Command](../xml-elements-properties/command-element-xmla.md)|  
|子元素|[ObjectDefinition](../xml-elements-properties/objectdefinition-element-xmla.md)， [ParentObject](../xml-elements-properties/object-element-xmla.md)|  
  
## <a name="attributes"></a>屬性  
  
|attribute|描述|  
|---------------|-----------------|  
|AllowOverwrite|選擇性`Boolean`屬性。 如果設定為 True，`ObjectDefinition` 元素中定義的物件就可以覆寫 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體上的現有物件。 如果這個屬性被省略或設定為 False，現有物件的存在就會產生錯誤。|  
|範圍。|選擇性`Enum`屬性。 定義 `ObjectDefinition` 元素中定義之物件的持續時間。 如果這屬性被省略，`ObjectDefinition` 元素中定義的物件就會保存在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體上。 有下列可用的值：<br /><br /> -   *工作階段*<br />     `ObjectDefinition` 元素中定義的物件只會在 XML for Analysis (XMLA) 工作階段的持續時間內存在。 **注意：** 時使用*工作階段*設定，`ObjectDefinition`元素只能包含[維度](../../scripting/objects/dimension-element-assl.md)， [Cube](../../scripting/objects/cube-element-assl.md)，或[MiningModel](../../scripting/objects/miningmodel-element-assl.md) ASSL 元素。|  
  
## <a name="remarks"></a>備註  
 每項 `Create` 作業都會在 `ParentObject` 元素提供的父系底下建立一個主要物件。 如果您了省略父物件，它就會被假設為目的地 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體。 如果主要物件的父系不是目的地執行個體，這樣做就會產生錯誤。  
  
## <a name="example"></a>範例  
 下列範例會在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體上建立名為 `Test Database` 的空白資料庫。  
  
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
 [命令&#40;XMLA&#41;](xml-elements-commands.md)  
  
  