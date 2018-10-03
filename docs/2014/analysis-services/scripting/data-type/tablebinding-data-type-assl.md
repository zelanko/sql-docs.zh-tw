---
title: TableBinding 資料類型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- TableBinding Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TableBinding
helpviewer_keywords:
- TableBinding data type
ms.assetid: 3195dca4-82bf-46b7-a31f-5383586e3573
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ab697a42fa489152801a98fb9791fcd657bc5762
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48059511"
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
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|[TabularBinding](binding-data-type-assl.md)|  
|衍生資料類型|None|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|None|  
|子元素|[DataSourceID](../properties/id-element-assl.md)， [DbSchemaName](../properties/name-element-assl.md)， [DbTableName](../properties/dbtablename-element-assl.md)|  
|衍生的元素|請參閱[繫結](binding-data-type-assl.md)|  
  
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
  
 計算運算式仍然適用，即使該運算式使用限定的資料表名稱 (例如 Sales.Qty) 也一樣。 如果此資料表改由某個查詢 "SELECT…" 取代，相同的情況會適用。上述 FROM 子句會成為 "FROM SELECT ...As Sales"。  
  
 如需詳細資訊`Binding`型別，包括資料表類型的 Analysis Services 指令碼語言 (ASSL) 物件`Binding`和繼承階層`Binding`類型，請參閱[繫結資料型別&#40;&#41;](binding-data-type-assl.md).  
  
 如需 ASSL 中資料繫結的概觀，請參閱 <<c0> [ 資料來源和繫結&#40;SSAS 多維度&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)。</c0>  
  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.TableBinding>。  
  
## <a name="see-also"></a>另請參閱  
 [繫結資料型別&#40;ASSL&#41;](binding-data-type-assl.md)   
 [資料來源和繫結&#40;SSAS 多維度&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)   
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
