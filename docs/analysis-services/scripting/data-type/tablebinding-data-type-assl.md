---
title: "TableBinding 資料類型 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
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
apiname: TableBinding Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: TableBinding
helpviewer_keywords: TableBinding data type
ms.assetid: 3195dca4-82bf-46b7-a31f-5383586e3573
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0d3e255d968e95d71813d28d71d12fb7284eb4fb
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="tablebinding-data-type-assl"></a>TableBinding 資料類型 (ASSL)
  定義代表資料表之繫結的衍生資料類型。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<TableBinding>  
   <!-- The following elements extend TabularBinding -->  
   <DataSourceID>...</DataSourceID>  
   <DbTableName>...</DbTableName>  
   <DbSchemaName>...</DbSchemaName>  
</TableBinding>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|說明|  
|--------------------|-----------------|  
|基底資料類型|[TabularBinding](../../../analysis-services/scripting/data-type/tabularbinding-data-type-assl.md)|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[DataSourceID](../../../analysis-services/scripting/properties/datasourceid-element-assl.md)， [DbSchemaName](../../../analysis-services/scripting/properties/dbschemaname-element-assl.md)， [DbTableName](../../../analysis-services/scripting/properties/dbtablename-element-assl.md)|  
|衍生的元素|請參閱[繫結](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
  
## <a name="remarks"></a>備註  
 請注意，利用子選擇在篩選運算式中參考其他資料表可能會在某些資料來源中產生效能隱含問題。 不過，設計師可以在資料來源檢視中定義具名查詢，然後參考該查詢，藉以完全控制 SQL 運算式。  
  
 定義資料分割之繫結的方法與在資料來源檢視中使用資料分割資料表無關。  
  
 例如，假設有一個量值群組，其預設資料表為 "Sales"，其中包含 Date、Product ID、Qty、Price 和 Amount 等資料行 (在資料來源檢視中計算)。 然後資料分割 "Sales97" 可能會使用資料表 "Sales97" 搭配篩選 "Year(Sales.Date) = 97"。  
  
 有效的查詢是：  
  
```  
SELECT Date, Product ID, Qty, Price, Qty * Price AS Amount   
   FROM Sales97 As Sales  
   WHERE Year(Sales.Date) = 97  
```  
  
 計算運算式仍然適用，即使該運算式使用限定的資料表名稱 (例如 Sales.Qty) 也一樣。 如果某個查詢的 [選取...] 取代資料表已改為，套用 上述 FROM 子句會成為"FROM SELECT...As Sales"。  
  
 如需有關**繫結**型別，包括資料表類型的 Analysis Services 指令碼語言 (ASSL) 物件**繫結**的繼承階層架構和**繫結**類型，請參閱[繫結資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/binding-data-type-assl.md).  
  
 如需 ASSL 中資料繫結的概觀，請參閱[資料來源和繫結 &#40;SSAS 多維度 &#41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.TableBinding>。  
  
## <a name="see-also"></a>請參閱＜  
 [繫結資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)   
 [資料來源和繫結 &#40;SSAS 多維度 &#41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)   
 [Analysis Services 指令碼語言 XML 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
