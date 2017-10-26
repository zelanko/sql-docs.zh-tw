---
title: "DbStorageLocation 元素 |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DbStorageLocation element
ms.assetid: 1f448249-103a-479f-ae86-b0017acd0436
caps.latest.revision: 15
author: jeannt
ms.author: jeannt
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9267f5858eb837efdbcd84fb040934e767835d4f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="dbstoragelocation-element"></a>DbStorageLocation 元素
  指定的資料夾位置[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]建立和管理所有資料庫資料和中繼資料檔案。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Database>  
...  
   <ddl100_100:DbStorageLocation>...</ddl100_100:DbStorageLocation>  
...  
</Database>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串|  
|預設值|""|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[資料庫](../../../analysis-services/xmla/xml-elements-properties/database-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 **DbStorageLocation** 資料庫屬性必須設定為現有的 UNC 資料夾路徑或空字串。 空字串是預設的伺服器資料夾。 執行時，如果資料夾不存在，會引發錯誤**建立**，**附加**，或**Alter**命令。  
  
 此外， **DbStorageLocation**資料庫屬性無法設定為指向伺服器資料夾或其任何子資料夾。 執行時，如果此位置指向伺服器資料夾或其任何子資料夾中，會引發錯誤**建立**，**附加**，或**Alter**命令。  
  
## <a name="see-also"></a>另請參閱  
 <xref:Microsoft.AnalysisServices.Database.DbStorageLocation%2A>   
 [附加和卸離 Analysis Services 資料庫](../../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)  
  
  

