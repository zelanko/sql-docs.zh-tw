---
title: MDDataSet 資料類型 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9b5f42140d8987cb36ea95c4c4314798a1ee7633
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="mddataset-data-type-xmla"></a>MDDataSet 資料類型 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  定義代表多維度資料所傳回的衍生的資料類型[Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法。  
  
 **命名空間**描述 urn:-microsoft-schemas-microsoft-com:-xml-analysis: mddataset  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<root xmlns="urn:schemas-microsoft-com:xml-analysis:rowset">  
   <!-- The following elements extend Resultset -->  
   <!-- Optional schema elements -->  
   <OlapInfo>...</OlapInfo>  
   <Axes>...</Axes>  
   <CellData>...</CellData>  
</root>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|說明|  
|--------------------|-----------------|  
|基底資料類型|[結果集](../../../analysis-services/xmla/xml-data-types/resultset-data-type-xmla.md)|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[座標軸](../../../analysis-services/xmla/xml-elements-properties/axes-element-xmla.md)， [CellData](../../../analysis-services/xmla/xml-elements-properties/celldata-element-xmla.md)， [OlapInfo](../../../analysis-services/xmla/xml-elements-properties/olapinfo-element-xmla.md)|  
|衍生的元素|無|  
  
## <a name="remarks"></a>備註  
 **MDDataSet**資料類型提供的 OLAP 導向資料列集 （或資料集） 表示在 XML 中的 OLAP 資料所需。 此資料列集的內容有所不同的值**內容**和**格式**提供的內容[屬性](../../../analysis-services/xmla/xml-elements-properties/properties-element-xmla.md)集合**執行**方法。 如需有關**內容**和**格式**屬性，請參閱[支援 XMLA 屬性&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md)。  
  
 如需有關 OLE DB for OLAP 資料集結構的基本資訊，請參閱 XML for Analysis 1.1 規格中的＜對應至 OLE DB 的 MDDataSet 資料類型＞。 針對完整的 XML 結構描述定義語言 (XSD) 範例**MDDataSet**資料類型，請參閱 「 附錄 D:mddataset 範例 > 的 XML for Analysis 1.1 規格。  
  
## <a name="see-also"></a>另請參閱  
 [XML 資料型別&#40;XMLA&#41;](../../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)  
  
  
