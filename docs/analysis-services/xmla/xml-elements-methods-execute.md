---
title: Execute 方法 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 56a48ffaf6d290d99503d7c8e1018f17e8d99a33
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="xml-elements---methods---execute"></a>XML 項目-方法-執行
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  將 XML for Analysis (XMLA) 命令傳送到的執行個體[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。 這包括涉及資料傳輸的要求，例如擷取或更新伺服器資料的要求。  
  
 **命名空間**描述 urn:-microsoft-schemas-microsoft-com:-分析  
  
 **SOAP 動作**」 描述 urn:-microsoft-schemas-microsoft-com:-分析： 執行 」  
  
## <a name="syntax"></a>語法  
  
```  
  
<Execute>  
   <Command>...</Command>  
   <Properties>...</Properties>  
   <Parameters>...</Parameters>  
</Execute>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-1：只出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[命令](../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)，[參數](../../analysis-services/xmla/xml-elements-properties/parameters-element-xmla.md)，[屬性](../../analysis-services/xmla/xml-elements-properties/properties-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 **Execute**方法執行 XMLA 命令中提供**命令**項目，並傳回任何產生的資料使用 XMLA[資料列集](../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md)（適用於表格式結果的資料類型設定） 或 XMLA [MDDataSet](../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md)資料類型 （適用於多維度結果集。）  
  
## <a name="example"></a>範例  
 下列程式碼範例是範例**Execute**包含多維度運算式 (MDX) SELECT 陳述式的方法呼叫。  
  
```  
<Execute xmlns="urn:schemas-microsoft-com:xml-analysis">  
   <Command>  
      <Statement>  
         SELECT [Measures].MEMBERS ON COLUMNS FROM [Adventure Works]  
      </Statement>  
   </Command>  
   <Properties>  
      <PropertyList>  
         <DataSourceInfo>Provider=MSOLAP;Data Source=local;</DataSourceInfo>  
         <Catalog>Adventure Works DW Multidimensional 2012</Catalog>  
         <Format>Multidimensional</Format>  
         <AxisFormat>ClusterFormat</AxisFormat>  
      </PropertyList>  
   </Properties>  
</Execute>  
```  
  
## <a name="see-also"></a>另請參閱  
 [XML 資料類型 & #40;XMLA & #41;](../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)   
 [Discover 方法&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-methods-discover.md)   
 [方法&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-methods.md)   
 [XML 項目 & #40;XMLA & #41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)   
 [Analysis Services 結構描述資料列集](../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)  
  
  
