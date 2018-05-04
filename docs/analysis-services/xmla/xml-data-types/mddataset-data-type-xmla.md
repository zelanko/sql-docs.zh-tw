---
title: MDDataSet 資料類型 (XMLA) |Microsoft 文件
ms.custom: ''
ms.date: 03/16/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- MDDataSet Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#MDDataSet
- MDDataSet
- urn:schemas-microsoft-com:xml-analysis#MDDataSet
helpviewer_keywords:
- MDDataSet data type
ms.assetid: 1a7e0092-f9f0-4ae5-ba27-ad1d8ebe8cb9
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 6b3fb82c79fd352df012a5fb5f800139f67a43be
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
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
  
  
