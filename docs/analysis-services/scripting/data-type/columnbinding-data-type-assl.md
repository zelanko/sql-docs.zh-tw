---
title: "ColumnBinding 資料類型 (ASSL) |Microsoft 文件"
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
apiname: ColumnBinding Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: ColumnBinding
helpviewer_keywords: ColumnBinding data type
ms.assetid: 3ab1bac1-6716-4b17-a107-d5f9c744c5e6
caps.latest.revision: "40"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 86d1f2ee2a1e389cc6d6d8a55b59815cc7546d06
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="columnbinding-data-type-assl"></a>ColumnBinding 資料類型 (ASSL)
  定義代表資料來源檢視中的資料行的繫結的衍生的資料類型[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ColumnBinding>  
   <!-- The following elements extend Binding -->  
   <TableID>...</TableID>  
      <ColumnID>...</ColumnID>  
</ColumnBinding>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|說明|  
|--------------------|-----------------|  
|基底資料類型|[繫結](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[ColumnID](../../../analysis-services/scripting/properties/columnid-element-eventcolumn-assl.md)， [TableID](../../../analysis-services/scripting/properties/tableid-element-assl.md)|  
|衍生的元素|請參閱[繫結](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
  
## <a name="remarks"></a>備註  
 若要建立有效的 XML 項目名稱[!INCLUDE[vstecado](../../../includes/vstecado-md.md)]**資料集**物件序列化至 XML 結構描述定義 (XSD) 時編碼資料表名稱; 例如，名稱"Order Details"會成為"Order_x0020_Details"。 同樣地， **ColumnID**和**TableID**所包含的項目**ColumnBinding**項目和資料來源檢視 (DSV) 中的參考物件也必須編碼在序列化期間，若要確保名稱直接與 DSV 中的文字的名稱。 Analysis Services 執行個體將會解碼這些名稱，就如同**資料集**物件模型。  
  
 A **TableDefinitions**元素所包含的項目使用**TableBinding**資料類型和參考資料表在 DSV 中必須也編碼名稱在序列化為 XSD。 不過，資料表名稱中**分割**應該編碼繫結，因為這些名稱只存在於資料庫中並不需要位於 DSV 中資料表名稱。 在不編碼資料表名稱**分割**繫結也會達成下列：  
  
-   它會讓資料分割的資料定義程式庫 (DDL) 更簡單。  
  
-   它會提供較佳的一致性，因為資料分割可以具有資料表名稱或 SELECT 陳述式，而且 SELECT 陳述式不應該進行編碼。  
  
 資料表和資料行名稱不會包含分隔符號 (例如，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的 "[")。  
  
 如需有關**繫結**型別，包括之 Analysis Services 指令碼語言 (ASSL) 物件的資料表**繫結**型別和繼承階層架構的**繫結**類型，請參閱[繫結資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/binding-data-type-assl.md).  
  
 如需 ASSL 中資料繫結的概觀，請參閱[資料來源和繫結 &#40;SSAS 多維度 &#41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 在 AMO 物件模型中的對應元素是 <xref:Microsoft.AnalysisServices.ColumnBinding>。  
  
## <a name="see-also"></a>請參閱＜  
 [Analysis Services 指令碼語言 XML 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
