---
title: DataSource 元素 (ASSL) |Microsoft 文件
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
- DataSource Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DataSource
helpviewer_keywords:
- DataSource element
ms.assetid: 113fba1c-2679-4d06-9339-90a4a76f9b31
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 5c87b21c6a9b291728704d3e624c386d59b820ef
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36035971"
---
# <a name="datasource-element-assl"></a>DataSource 元素 (ASSL)
  定義中的資料來源[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] [資料庫](database-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DataSources>  
   <DataSource xsi:type="RelationalDataSource">...</DataSource>  
   <!-- or -->  
   <DataSource xsi:type="OlapDataSource">...</DataSource>  
   <!-- or -->  
   <DataSource xsi:type="PushedDataSource">...</DataSource>  
</DataSources>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|[RelationalDataSource](../data-type/datasource-data-type-assl.md)， [OlapDataSource](../data-type/olapdatasource-data-type-assl.md)， [PushedDataSource](../data-type/pusheddatasource-data-type-assl.md)|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[資料來源](../collections/datasources-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.DataSource>。  
  
## <a name="see-also"></a>另請參閱  
 [Database 元素&#40;ASSL&#41;](database-element-assl.md)   
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  