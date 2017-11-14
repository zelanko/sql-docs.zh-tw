---
title: "結構描述元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Schema Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Schema
helpviewer_keywords:
- Schema element
ms.assetid: 4b6375fb-7ad8-4d5f-88b1-abd3da2654db
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 51fd142bad60a7c8e64d27952509dfa5b2b6c28f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="schema-element-assl"></a>Schema 元素 (ASSL)
  包含資料來源檢視的結構描述。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DataSourceView>  
   ...  
   <Schema>...</Schema>  
   ...  
</DataSourceView>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|結構描述|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 **結構描述**，則使用中的資料集的 XML 結構描述定義 (XSD) 語言格式表示[!INCLUDE[msCoName](../../../includes/msconame-md.md)].NET Framework，以及資料集和其他特定的資料定義內部使用的一些擴充功能語言 (DDL)。 雖然 DataSet 會定義 XSD 與關聯式結構描述之間的彈性對應，但是之後會以更標準的格式傳回 XSD。 只有這個標準格式在資料來源中有效。  
  
 對應目的父代的項目**結構描述**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.DataSourceView>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

