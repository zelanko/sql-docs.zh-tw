---
title: TableID 元素 (ASSL) |Microsoft 文件
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
- TableID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TableID
helpviewer_keywords:
- TableID element
ms.assetid: 45fe7e23-b274-4bc2-be63-1a5bb6680f51
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 9b8f85ee3fecac1b098a16afe6cf2d0eca61226b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36146828"
---
# <a name="tableid-element-assl"></a>TableID 元素 (ASSL)
  包含資料表的識別碼 (ID) (從[DataSourceView](../objects/datasourceview-element-assl.md)項目) 與父元素相關聯。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ColumnBinding> <!-- or DSVTableBinding, RowBinding, IncrementalProcessingNotification -->  
   ...  
   <TableID>...</TableID>  
   ...  
</ColumnBinding>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[ColumnBinding](../data-type/binding-data-type-assl.md)， [DSVTableBinding](../data-type/tablebinding-data-type-assl.md)， [IncrementalProcessingNotification](../objects/incrementalprocessingnotification-element-assl.md)， [RowBinding](../data-type/rowbinding-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 由 `TableID` 所識別的資料表必須位於主控物件 (維度或 Cube) 所繫結的資料來源中。  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `TableID` 父系的元素是 <xref:Microsoft.AnalysisServices.ColumnBinding>、<xref:Microsoft.AnalysisServices.DSVTableBinding>、<xref:Microsoft.AnalysisServices.IncrementalProcessingNotification> 和 <xref:Microsoft.AnalysisServices.RowBinding>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  