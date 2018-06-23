---
title: MDDataSet 資料類型 (XMLA) |Microsoft 文件
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
- MDDataSet Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
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
manager: mblythe
ms.openlocfilehash: 098a123c28e4a449ad6425d1a74ff8355d074e08
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024053"
---
# <a name="mddataset-data-type-xmla"></a>MDDataSet 資料類型 (XMLA)
  定義代表多維度資料所傳回的衍生的資料類型[Execute](../xml-elements-methods-execute.md)方法。  
  
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
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|[結果集](resultset-data-type-xmla.md)|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[座標軸](../xml-elements-properties/axes-element-xmla.md)， [CellData](../xml-elements-properties/celldata-element-xmla.md)， [OlapInfo](../xml-elements-properties/olapinfo-element-xmla.md)|  
|衍生的元素|無|  
  
## <a name="remarks"></a>備註  
 `MDDataSet` 資料類型會提供以 XML 表示 OLAP 資料所需的 OLAP 導向資料列集 (或資料集)。 此資料列集的內容有所不同的值`Content`和`Format`提供的內容[屬性](../xml-elements-properties/properties-element-xmla.md)集合`Execute`方法。 如需有關`Content`和`Format`屬性，請參閱[支援 XMLA 屬性&#40;XMLA&#41;](../xml-elements-properties/propertylist-element-supported-xmla-properties.md)。  
  
 如需有關 OLE DB for OLAP 資料集結構的基本資訊，請參閱 XML for Analysis 1.1 規格中的＜對應至 OLE DB 的 MDDataSet 資料類型＞。 如需 `MDDataSet` 資料類型的完整 XML 結構描述定義語言 (XSD) 範例，請參閱 XML for Analysis 1.1 規格的＜附錄 D：MDDataSet 範例＞。  
  
## <a name="see-also"></a>另請參閱  
 [XML 資料型別&#40;XMLA&#41;](xml-data-types-xmla.md)  
  
  