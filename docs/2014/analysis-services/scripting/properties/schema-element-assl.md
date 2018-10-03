---
title: 結構描述元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Schema Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Schema
helpviewer_keywords:
- Schema element
ms.assetid: 4b6375fb-7ad8-4d5f-88b1-abd3da2654db
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5b8f9ab11698c2e0e73436abb3506ca38c45afe6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48218791"
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
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|結構描述|  
|預設值|None|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[DataSourceView](../objects/datasourceview-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 `Schema` 是使用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 中 DataSet 的 XML 結構描述定義 (XSD) 語言格式表示，而且具有 DataSet 的某些延伸模組和在資料定義語言 (DDL) 內部使用的專用延伸模組。 雖然 DataSet 會定義 XSD 與關聯式結構描述之間的彈性對應，但是之後會以更標準的格式傳回 XSD。 只有這個標準格式在資料來源中有效。  
  
 對應至父系的元素`Schema`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.DataSourceView>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
