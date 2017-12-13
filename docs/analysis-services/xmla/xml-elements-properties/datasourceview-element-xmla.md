---
title: "DataSourceView 元素 (XMLA) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
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
apiname: DataSourceView Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#DataSourceView
- microsoft.xml.analysis.datasourceview
- urn:schemas-microsoft-com:xml-analysis#DataSourceView
helpviewer_keywords: DataSourceView element
ms.assetid: c4a4360f-7342-484b-bac1-0a247e8f279d
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8d4516694011712336c7c2063a83d9945a6977ad
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="datasourceview-element-xmla"></a>DataSourceView 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]包含父繫結超出 (out-of-line） 資料來源檢視[批次](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)或[程序](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Batch> <!-- or Process>  
...  
   <DataSourceView>  
      <DatabaseID>...</DatabaseID>  
      <DataSourceViewID>...</DataSourceViewID>  
   </DataSourceView>  
...  
</Batch>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[批次](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)，[程序](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)|  
|子元素|[DatabaseID](../../../analysis-services/xmla/xml-elements-properties/databaseid-element-xmla.md)， [DataSourceViewID](../../../analysis-services/scripting/properties/datasourceviewid-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 **DataSourceView**項目表示-單行的繫結到資料來源檢視，供**批次**或**程序**命令來暫時覆寫資料來源檢視繫結[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]命令所處理的物件。  
  
 單行繫結的詳細資訊，請參閱[資料來源和繫結 &#40;SSAS 多維度 &#41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
## <a name="see-also"></a>請參閱  
 [屬性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
