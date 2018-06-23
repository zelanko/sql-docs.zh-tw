---
title: 結構描述元素 (ASSL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 130d1363a007fb51db3bc7b39efcae4d9140c368
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36037566"
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
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[DataSourceView](../objects/datasourceview-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 `Schema` 是使用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 中 DataSet 的 XML 結構描述定義 (XSD) 語言格式表示，而且具有 DataSet 的某些延伸模組和在資料定義語言 (DDL) 內部使用的專用延伸模組。 雖然 DataSet 會定義 XSD 與關聯式結構描述之間的彈性對應，但是之後會以更標準的格式傳回 XSD。 只有這個標準格式在資料來源中有效。  
  
 對應目的父代的項目`Schema`在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.DataSourceView>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  