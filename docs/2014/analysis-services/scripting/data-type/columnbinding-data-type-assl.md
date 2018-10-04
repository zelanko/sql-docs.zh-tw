---
title: ColumnBinding 資料類型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ColumnBinding Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ColumnBinding
helpviewer_keywords:
- ColumnBinding data type
ms.assetid: 3ab1bac1-6716-4b17-a107-d5f9c744c5e6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 271b4ae8b305e554f94bd1b0da3bbed96a7dd476
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48149338"
---
# <a name="columnbinding-data-type-assl"></a>ColumnBinding 資料類型 (ASSL)
  定義代表資料來源檢視中的資料行的繫結的衍生的資料類型[DataItem](dataitem-data-type-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ColumnBinding>  
   <!-- The following elements extend Binding -->  
   <TableID>...</TableID>  
      <ColumnID>...</ColumnID>  
</ColumnBinding>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|[繫結](binding-data-type-assl.md)|  
|衍生資料類型|None|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|None|  
|子元素|[ColumnID](../properties/columnid-element-eventcolumn-assl.md)， [TableID](../properties/id-element-assl.md)|  
|衍生的元素|請參閱[繫結](binding-data-type-assl.md)|  
  
## <a name="remarks"></a>備註  
 若要建立有效的 XML 項目名稱[!INCLUDE[vstecado](../../../includes/vstecado-md.md)]`DataSet`物件序列化為 XML 結構描述定義 (XSD) 時編碼資料表名稱; 例如，名稱"Order Details"會成為"Order_x0020_Details"。 同樣地，`ColumnID` 元素所包含的 `TableID` 和 `ColumnBinding` 元素 (在資料來源檢視 (DSV) 中參考物件) 也必須在序列化過程中編碼名稱，以便確保這些名稱直接與 DSV 中的文字相符。 Analysis Services 執行個體將會解碼這些名稱，如同 `DataSet` 物件模型所做的。  
  
 使用 `TableDefinitions` 資料類型之元素所包含的 `TableBinding` 元素 (在 DSV 中參考資料表) 也必須在序列化為 XSD 時編碼名稱。 不過，`Partition` 繫結中的資料表名稱不應該進行編碼，因為這些名稱只是存在資料庫中而不需要位於 DSV 中之資料表的名稱。 沒有編碼 `Partition` 繫結中的資料表名稱也會達到下列效果：  
  
-   它會讓資料分割的資料定義程式庫 (DDL) 更簡單。  
  
-   它會提供較佳的一致性，因為資料分割可以具有資料表名稱或 SELECT 陳述式，而且 SELECT 陳述式不應該進行編碼。  
  
 資料表和資料行名稱不會包含分隔符號 (例如，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的 "[")。  
  
 如需詳細資訊`Binding`型別，包括之 Analysis Services 指令碼語言 (ASSL) 物件的資料表`Binding`型別和繼承階層`Binding`類型，請參閱[繫結資料型別&#40;ASSL&#41;](binding-data-type-assl.md)。  
  
 如需 ASSL 中資料繫結的概觀，請參閱 <<c0> [ 資料來源和繫結&#40;SSAS 多維度&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)。</c0>  
  
 在 AMO 物件模型中的對應元素是 <xref:Microsoft.AnalysisServices.ColumnBinding>。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
