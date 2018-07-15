---
title: 資料格元素 (MDDataSet) (XMLA) |Microsoft Docs
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
- Cell Element (MDDataSet)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.cell
- http://schemas.microsoft.com/analysisservices/2003/engine#Cell
- urn:schemas-microsoft-com:xml-analysis#Cell
helpviewer_keywords:
- Cell element
ms.assetid: c4ea08a4-f653-4ade-be07-b91eb5b1ef32
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3f07798a28c59597575de08bf5d0f3ea1d7087c8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37269504"
---
# <a name="cell-element-mddataset-xmla"></a>Cell 元素 (MDDataSet) (XMLA)
  包含父代所包含的單一儲存格的相關資訊[CellData](celldata-element-xmla.md)項目。  
  
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
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[CellData](celldata-element-xmla.md)|  
|子元素|零或多個資料格屬性值或[錯誤](error-element-xmla.md)|  
  
## <a name="attributes"></a>屬性  
  
|attribute|描述|  
|---------------|-----------------|  
|CellOrdinal|所需`unsignedInt`屬性。 資料格在多維度資料集中的序數位置。|  
  
## <a name="remarks"></a>備註  
 在 `root` 父元素中，`Axes` 元素後面接著 `CellData` 元素，而它是 `Cell` 元素的集合，其中包含在多維度資料集中傳回之每個資料格的屬性值。 `Cell` 元素包含 `CellOrdinal` 屬性 (Attribute)，它會指出資料格在多維度資料集中的以零為基底序數位置，而且會針對與資料格相關聯的每個資料格屬性 (Property) 值指出一個元素。 `Cell` 元素中的每個資料格屬性值都由不同的 XML 元素所定義。 資料格屬性的值是 XML 元素所包含的資料，而且資料格屬性的名稱 (在父根元素的 `CellInfo` 元素中定義) 會對應至 XML 元素的名稱。  
  
 下列語法將描述資料格屬性值：  
  
```  
<CellProperty xsi:type="string">value</CellProperty>  
```  
  
 資料格屬性值的資料類型僅針對 VALUE 資料格屬性指定。 其他資料格屬性的資料類型則由 `CellInfo` 元素中包含的資料格屬性定義決定。 如果您已經針對資料格屬性指定預設值 (針對 `Default` 元素中包含的資料格屬性定義加入 `CellInfo` 元素)，或者沒有指定任何預設值而且資料格屬性的值為 Null，此時可能會排除資料格屬性值元素。  
  
## <a name="cell-property-errors"></a>資料格屬性錯誤  
 若無法傳回資料格屬性，因為執行個體，就會發生錯誤，所以[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，例如防止針對指定的資料格，傳回值的計算錯誤`Error`取代項目有問題的資料格屬性內容。 下列 XML 範例將描述資料格屬性錯誤：  
  
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
 您可以根據 `CellOrdinal` 屬性值來計算資料格的軸參考。 就概念而言，儲存格編號資料集內，好像資料集*p*-維陣列，其中*p*是軸的數目。 資料格的處理順序是以資料列為主。  
  
 假設某項查詢針對資料行要求四個量值，而針對資料列要求兩個州與四個季節的交叉聯結。 在下列資料集結果中，以粗體文字顯示之資料集結果部分的 `CellOrdinal` 屬性為 {9, 10, 11, 13, 14, 15, 17, 18, 19} 集合。 這是集合，因為這些資料格的編號順序是以資料列為主，從 `CellOrdinal` 0 (代表左上資料格) 開始。  
  
|State|Quarter|單位銷售量|店面成本|店面銷售量|銷售計數|  
|-----------|-------------|----------------|----------------|-----------------|-----------------|  
|California|Q1|16890|14431.09|36175.2|5498|  
||第 2 季|18052|15332.02|38396.75|5915|  
||第 3 季|18370|**15672.83**|**39394.05**|**6014**|  
||Q4|21436|**18094.5**|**45201.84**|**7015**|  
|Oregon|Q1|19287|**16081.07**|**40170.29**|**6184**|  
||第 2 季|15079|12678.96|31772.88|4799|  
||第 3 季|16940|14273.78|35880.46|5432|  
||Q4|16353|13738.68|34453.44|5196|  
|Washington|Q1|30114|25240.08|63282.86|9906|  
||第 2 季|29479|24953.25|62496.64|9654|  
||第 3 季|30538|25958.26|64997.38|10007|  
||Q4|34235|29172.72|73016.34|11217|  
  
 套用本圖所示的公式後，軸 k = 0 具有 Uk = 4 個成員，而軸 k = 1 具有 Uk = 8 個 Tuple。 P = 2 是查詢中的總軸數。 將資料格 {California, Q3, Store Cost} 視為 S0 之後，初始總和為 i = 0 至 1。 若 i = 0，{Store Cost} 之軸 0 上的 Tuple 序數是 1。 若 i = 1，{CA, Q3} 的 Tuple 序數則為 2。  
  
 如我 = 0，則 Ei = 1，因此我 = 0 總和為 1 * 1 = 1 和我 = 1，則總和為 2 (tuple 序數) 乘以 4 (的 Ei 值計算為 1 \* 4)，或 8。 1 + 8 的總和為 9，亦即該資料格的資料格序數。  
  
## <a name="example"></a>範例  
 下列範例將示範 `Cell` 元素的結構，包括每個資料格的 VALUE、FORMATTED_VALUE 和 FORMAT_STRING 資料格屬性值。  
  
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
  
## <a name="see-also"></a>另請參閱  
 [MDDataSet 資料類型&#40;XMLA&#41;](../xml-data-types/mddataset-data-type-xmla.md)   
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
