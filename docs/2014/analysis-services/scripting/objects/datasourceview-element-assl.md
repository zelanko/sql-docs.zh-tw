---
title: DataSourceView 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DataSourceView Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DataSourceView
helpviewer_keywords:
- DataSourceView element
ms.assetid: cda26126-8af2-4519-8237-f4a57976a284
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3715cb626f885096520c10682fa119f65b867ce2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48187968"
---
# <a name="datasourceview-element-assl"></a>DataSourceView 元素 (ASSL)
  定義所使用的資料來源檢視[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] [資料庫](database-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DataSourceViews>  
   <DataSourceView>  
      <Name>...</Name>  
      <ID>...</ID>  
      <CreatedTimestamp>...</CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <Description>...</Description>  
      <Annotations>...</Annotations>  
      <DataSourceID>   </DataSourceID>  
      <Schema>...</Schema>  
   </DataSourceView>  
</DataSourceViews>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|None|  
|預設值|None|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[DataSourceViews](../collections/datasourceviews-element-assl.md)|  
|子元素|[註釋](../collections/annotations-element-assl.md)， [CreatedTimestamp](../properties/createdtimestamp-element-assl.md)， [DataSourceID](../properties/id-element-assl.md)，[描述](../properties/description-element-assl.md)，[識別碼](../properties/id-element-assl.md)， [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md)，[名稱](../properties/name-element-assl.md)，[結構描述](../properties/schema-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.DataSourceView>。  
  
## <a name="see-also"></a>另請參閱  
 [資料庫項目&#40;ASSL&#41;](database-element-assl.md)   
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  
