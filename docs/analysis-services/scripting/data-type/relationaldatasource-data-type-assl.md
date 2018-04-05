---
title: RelationalDataSource 資料類型 (ASSL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- RelationalDataSource Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- RelationalDataSource
helpviewer_keywords:
- RelationalDataSource data type
ms.assetid: 2b99d7d0-731d-4506-8c37-678a5dc29c8a
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 580ebe449b555b7ed649255865e21b6ba02c49e8
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="relationaldatasource-data-type-assl"></a>RelationalDataSource 資料類型 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]定義衍生的資料類型，表示[DataSource](../../../analysis-services/scripting/objects/datasource-element-assl.md)關聯式資料來源為基礎的項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<RelationalDataSource>  
   <!-- Child elements are only those inherited from DataSource -->  
</RelationalDataSource>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|[資料來源](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md)|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|無|  
|衍生的元素|[資料來源](../../../analysis-services/scripting/objects/datasource-element-assl.md)([DataSources](../../../analysis-services/scripting/collections/datasources-element-assl.md)集合[資料庫](../../../analysis-services/scripting/objects/database-element-assl.md))|  
  
## <a name="remarks"></a>備註  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.RelationalDataSource>。  
  
## <a name="see-also"></a>請參閱  
 [Analysis Services 指令碼語言 XML 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
