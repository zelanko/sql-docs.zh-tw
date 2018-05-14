---
title: TableBinding 資料類型 (ASSL) |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 80055d443f0a08b7cc957d5fa26d458178d3a1f6
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="tablebinding-data-type-assl"></a>TableBinding 資料類型 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
 如需有關**繫結**型別，包括資料表類型的 Analysis Services 指令碼語言 (ASSL) 物件**繫結**的繼承階層架構和**繫結**類型，請參閱[繫結資料型別&#40;ASSL&#41;](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)。  
  
 如需 ASSL 中資料繫結的概觀，請參閱[資料來源和繫結 & #40;SSAS 多維度 & #41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.TableBinding>。  
  
## <a name="see-also"></a>另請參閱  
 [繫結資料類型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)   
 [資料來源和繫結&#40;SSAS 多維度&#41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)   
 [Analysis Services 指令碼語言 XML 資料類型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
