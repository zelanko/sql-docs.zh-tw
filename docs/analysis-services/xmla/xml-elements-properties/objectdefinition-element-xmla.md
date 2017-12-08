---
title: "ObjectDefinition 元素 (XMLA) |Microsoft 文件"
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
apiname: ObjectDefinition Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#ObjectDefinition
- http://schemas.microsoft.com/analysisservices/2003/engine#ObjectDefinition
- microsoft.xml.analysis.objectdefinition
helpviewer_keywords: ObjectDefinition element
ms.assetid: 1911868c-a018-4308-8cf9-972a57f610a1
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9dfdfbf039d9c6f4dde19f89c7cb1d5326339491
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="objectdefinition-element-xmla"></a>ObjectDefinition 元素 (XMLA)
  包含一或多個 Analysis Services 指令碼語言 (ASSL) 元素，用來建立或更改物件的執行個體上[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Create> <!-- or Alter -->  
   ...  
   <ObjectDefinition>  
      <!-- One or more ASSL elements -->  
   </ObjectDefinition>  
   ...  
</Create>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Alter](../../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)，[建立](../../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)|  
|子元素|必要的 ASSL 元素。 一個或多個可用來定義 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 物件的 ASSL 元素。 如需有關 ASSL 的詳細資訊，請參閱[屬性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md).|  
  
## <a name="remarks"></a>備註  
  
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
  
## <a name="see-also"></a>請參閱＜  
 [屬性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
