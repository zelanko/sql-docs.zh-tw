---
title: DataSourceType 元素 (XMLA) |Microsoft 文件
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
- DataSourceType Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#DataSourceType
- microsoft.xml.analysis.datasourcetype
- http://schemas.microsoft.com/analysisservices/2003/engine#DataSourceType
helpviewer_keywords:
- DataSourceType element
ms.assetid: f5a348b1-911b-4139-832e-4bcb6d80a728
caps.latest.revision: 12
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: cc083742521abfe9114ea474fe0987861d12c04e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36035962"
---
# <a name="datasourcetype-element-xmla"></a>DataSourceType 元素 (XMLA)
  指出是否[位置](location-element-xmla.md)指定的項目[還原](../xml-elements-commands/restore-element-xmla.md)或[Synchronize](../xml-elements-commands/synchronize-element-xmla.md)命令在本機或遠端。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Location>  
   ...  
   <DataSourceType>...</DataSourceType>  
   ...  
</Location>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*遠端*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[位置](location-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 `DataSourceType` 元素會決定 `Location` 元素所定義的資料來源包含本機資料來源或遠端資料來源。 如需有關備份和還原遠端資料分割的詳細資訊，請參閱[備份、 還原及同步處理資料庫&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)。  
  
 這個元素的值限制為下表所列的其中一個字串。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|*本機*|`Location` 元素會定義本機資料來源。 如果您使用這個值，`Restore` 和 `Synchronize` 命令就會使用 `Location` 元素中定義的資訊來更新 `File` 元素之 `Backup` 元素中識別的資料來源 (擷取自 `Source` 命令之 `Synchronize` 元素中指定的備份檔案或 `DataSourceID` 命令之 `Location` 元素中指定的資料庫)。<br /><br /> 這個值允許使用關聯式 OLAP (ROLAP) 儲存的物件在還原或同步處理之後，針對其資料和中繼資料使用不同的資料庫。 **注意：** 不還原或同步處理 ROLAP 資料，例如維度資料表或回寫資料表中的資料。 只有 ROLAP 物件的中繼資料會進行還原或同步處理。|  
|*遠端*|`Location` 元素會定義遠端資料來源。 如果您使用這個值，`Restore` 和 `Synchronize` 命令就會使用 `Location` 元素中定義的資訊，將遠端資料分割 (擷取自 `File` 命令之 `Backup` 元素中指定的備份檔案或 `Source` 命令之 `Synchronize` 元素中指定的資料庫) 還原或同步處理至 `DataSourceID` 元素之 `Location` 中識別的遠端執行個體。|  
  
## <a name="see-also"></a>另請參閱  
 [ConnectionString 元素&#40;XMLA&#41;](connectionstring-element-xmla.md)   
 [DataSourceID 元素&#40;XMLA&#41;](id-element-xmla.md)   
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  