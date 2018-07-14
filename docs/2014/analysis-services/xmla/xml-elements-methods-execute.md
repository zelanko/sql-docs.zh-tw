---
title: Execute 方法 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Execute Method
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- EXECUTE
- urn:schemas-microsoft-com:xml-analysis#
- http://schemas.microsoft.com/analysisservices/2003/engine#
- microsoft.xml.analysis.execute
- urn:schemas-microsoft-com:xml-analysis#Execute
helpviewer_keywords:
- Execute method
ms.assetid: 0fff5221-7164-4bbc-ab58-49cf04c52664
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ec3fa458148638af5431b4a519acf8556d29b122
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37235558"
---
# <a name="execute-method-xmla"></a>Execute 方法 (XMLA)
  將 XML for Analysis (XMLA) 命令傳送到的執行個體[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。 這包括涉及資料傳輸的要求，例如擷取或更新伺服器資料的要求。  
  
 **命名空間**urn: schemas-microsoft-microsoft-schemas-microsoft-com:-分析  
  
 **SOAP 動作**"urn: schemas-microsoft-microsoft-schemas-microsoft-com:-分析： 執行 」  
  
## <a name="syntax"></a>語法  
  
```  
  
<Execute>  
   <Command>...</Command>  
   <Properties>...</Properties>  
   <Parameters>...</Parameters>  
</Execute>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-1：只出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[命令](xml-elements-properties/command-element-xmla.md)，[參數](xml-elements-properties/parameters-element-xmla.md)，[屬性](xml-elements-properties/properties-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 `Execute`方法會執行 XMLA 命令中提供`Command`項目，並傳回任何產生的資料，使用 XMLA[資料列集](xml-data-types/rowset-data-type-xmla.md)（適用於表格式結果集） 的資料型別或 XMLA [MDDataSet](xml-data-types/mddataset-data-type-xmla.md)資料類型 （適用於多維度結果集。）  
  
## <a name="example"></a>範例  
 下列程式碼範例是包含多維度運算式 (MDX) SELECT 陳述式之 `Execute` 方法呼叫的範例。  
  
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
 [XML 資料型別&#40;XMLA&#41;](xml-data-types/xml-data-types-xmla.md)   
 [探索方法&#40;XMLA&#41;](xml-elements-methods-discover.md)   
 [方法&#40;XMLA&#41;](xml-elements-methods.md)   
 [XML 項目&#40;XMLA&#41;](../dev-guide/xml-elements-xmla.md)   
 [Analysis Services 結構描述資料列集](../schema-rowsets/analysis-services-schema-rowsets.md)  
  
  
