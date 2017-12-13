---
title: "資料格元素 (MDDataSet) (XMLA) |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Cell Element (MDDataSet)
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.cell
- http://schemas.microsoft.com/analysisservices/2003/engine#Cell
- urn:schemas-microsoft-com:xml-analysis#Cell
helpviewer_keywords: Cell element
ms.assetid: c4ea08a4-f653-4ade-be07-b91eb5b1ef32
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 5c90aca85496cfe59b18a93230cb5157052eaacf
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="cell-element-mddataset-xmla"></a>Cell 元素 (MDDataSet) (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]包含父代所包含的單一資料格的相關資訊[CellData](../../../analysis-services/xmla/xml-elements-properties/celldata-element-xmla.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<CellData>  
   <Cell CellOrdinal="unsignedInt">  
      <!-- Zero or more cell property values -->  
      <!-- or -->  
      <Error>...</Error>  
   </Cell>  
</CellData>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[CellData](../../../analysis-services/xmla/xml-elements-properties/celldata-element-xmla.md)|  
|子元素|零或多個資料格屬性值或[錯誤](../../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md)|  
  
## <a name="attributes"></a>屬性  
  
|Attribute|說明|  
|---------------|-----------------|  
|CellOrdinal|需要**unsignedInt**屬性。 資料格在多維度資料集中的序數位置。|  
  
## <a name="remarks"></a>備註  
 與父系**根**項目，**座標軸**元素後面**CellData**元素中，集合**儲存格**包含的項目傳回多維度資料集中每個資料格屬性值。 **儲存格**元素包含**CellOrdinal**屬性，表示資料格在多維度資料集，並針對每個資料格屬性值的一個項目以零為起始的序數位置儲存格相關聯。 中的每個資料格屬性值**儲存格**項目由不同的 XML 元素所定義。 資料格屬性的值是 XML 項目和資料格屬性的名稱中包含的資料，如中所定義**CellInfo**父根項目，項目對應至 XML 項目的名稱。  
  
 下列語法將描述資料格屬性值：  
  
```  
<CellProperty xsi:type="string">value</CellProperty>  
```  
  
 資料格屬性值的資料類型僅針對 VALUE 資料格屬性指定。 資料類型的其他資料格屬性由包含在資料格屬性定義**CellInfo**項目。 資料格屬性值項目可能會排除在指定的預設值 (包含**預設**資料格屬性定義中所包含的項目**CellInfo**項目) 為資料格的屬性，或如果已指定沒有預設值，而且資料格屬性的值為 null。  
  
## <a name="cell-property-errors"></a>資料格屬性錯誤  
 如果資料格屬性不能傳回的執行個體發生的錯誤，因為[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，例如防止針對給定的資料格，傳回值的計算錯誤**錯誤**項目會取代所討論的資料格屬性的內容。 下列 XML 範例將描述資料格屬性錯誤：  
  
```  
<Cell CellOrdinal="0">  
   <Value xsi:type="xsd:double">  
      <Error>  
         <ErrorCode>2148497527</ErrorCode>  
         <Description>Unknown error</Description>  
      </Error>  
   </Value>  
</Cell>  
```  
  
## <a name="calculating-cell-ordinal-values"></a>計算資料格序數值  
 軸參考儲存格可計算根據**CellOrdinal**屬性值。 在概念上，方格的編號是集中如同資料集是*p*-維陣列，其中*p*是軸的數目。 資料格的處理順序是以資料列為主。  
  
 假設某項查詢針對資料行要求四個量值，而針對資料列要求兩個州與四個季節的交叉聯結。 下列資料集結果中**CellOrdinal**以粗體字顯示的資料集結果部分屬性是 {9、 10、 11、 13、 14、 15、 17、 18，19} 集合。 這是集合，因為資料格會以列為主要順序編號開頭**CellOrdinal**為 0，表示左上資料格。  
  
|State|Quarter|單位銷售量|店面成本|店面銷售量|銷售計數|  
|-----------|-------------|----------------|----------------|-----------------|-----------------|  
|California|Q1|16890|14431.09|36175.2|5498|  
||Q2|18052|15332.02|38396.75|5915|  
||Q3|18370|**15672.83**|**39394.05**|**6014**|  
||Q4|21436|**18094.5**|**45201.84**|**7015**|  
|Oregon|Q1|19287|**16081.07**|**40170.29**|**6184**|  
||Q2|15079|12678.96|31772.88|4799|  
||Q3|16940|14273.78|35880.46|5432|  
||Q4|16353|13738.68|34453.44|5196|  
|Washington|Q1|30114|25240.08|63282.86|9906|  
||Q2|29479|24953.25|62496.64|9654|  
||Q3|30538|25958.26|64997.38|10007|  
||Q4|34235|29172.72|73016.34|11217|  
  
 套用本圖所示的公式後，軸 k = 0 具有 Uk = 4 個成員，而軸 k = 1 具有 Uk = 8 個 Tuple。 P = 2 是查詢中的總軸數。 將資料格 {California, Q3, Store Cost} 視為 S0 之後，初始總和為 i = 0 至 1。 若 i = 0，{Store Cost} 之軸 0 上的 Tuple 序數是 1。 若 i = 1，{CA, Q3} 的 Tuple 序數則為 2。  
  
 為我 = 0，則 Ei = 1，因此我 = 0 總和為 1 * 1 = 1 和我 = 1，則總和為 2 (tuple 序數) 乘以 4 (的 Ei 值計算為 1 \* 4)，或 8。 1 + 8 的總和為 9，亦即該資料格的資料格序數。  
  
## <a name="example"></a>範例  
 下列範例示範結構**儲存格**項目，包括值、 FORMATTED_VALUE 和 FORMAT_STRING 資料格的每個資料格屬性值。  
  
```  
<CellData>  
   <Cell CellOrdinal="0">  
      <Value xsi:type="xsd:double">16890</Value>  
      <FmtValue>16,890.00</FmtValue>  
      <FormatString>Standard</FormatString>  
   </Cell>  
   <Cell CellOrdinal="1">  
      <Value xsi:type="xsd:int">50</Value>  
      <FmtValue>50</FmtValue>  
      <FormatString>Standard</FormatString>  
   </Cell>  
   <Cell CellOrdinal="2">  
      <Value xsi:type="xsd:double">36175.2</Value>  
      <FmtValue>$36,175.20</FmtValue>  
      <FormatString>Currency</FormatString>  
   </Cell>  
</CellData>  
```  
  
## <a name="see-also"></a>請參閱  
 [MDDataSet 資料類型 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md)   
 [屬性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
