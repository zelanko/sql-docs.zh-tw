---
title: DataSourceID 元素 (XMLA) |Microsoft 文件
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
- DataSourceID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.datasourceid
- urn:schemas-microsoft-com:xml-analysis#DataSourceID
- http://schemas.microsoft.com/analysisservices/2003/engine#DataSourceID
helpviewer_keywords:
- DataSourceID element
ms.assetid: 695522c7-acca-420a-a5fb-f01f3fd9a96b
caps.latest.revision: 12
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 2adec20f28e51639352dc89c70b6682e4df240fc
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36131792"
---
# <a name="datasourceid-element-xmla"></a>DataSourceID 元素 (XMLA)
  識別所使用的資料來源[位置](location-element-xmla.md)項目期間[備份](../xml-elements-commands/backup-element-xmla.md)，[還原](../xml-elements-commands/restore-element-xmla.md)，或[Synchronize](../xml-elements-commands/synchronize-element-xmla.md)命令。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Location>  
   ...  
   <DataSourceID>...</DataSourceID>  
   ...  
</Location>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[位置](location-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 `DataSourceID` 元素包含來源執行個體之資料來源的名稱，可識別要在上面備份、還原或同步處理遠端資料分割資訊的遠端執行個體。  
  
 如需有關備份和還原遠端資料分割的詳細資訊，請參閱[備份、 還原及同步處理資料庫&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)。  
  
## <a name="see-also"></a>另請參閱  
 [ConnectionString 元素&#40;XMLA&#41;](connectionstring-element-xmla.md)   
 [DataSourceType 元素&#40;XMLA&#41;](type-element-xmla.md)   
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  