---
title: DbStorageLocation 元素 |Microsoft Docs
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
helpviewer_keywords:
- DbStorageLocation element
ms.assetid: 1f448249-103a-479f-ae86-b0017acd0436
caps.latest.revision: 15
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 055780c9c91817a44dce6dfdaeb6ea3b541c05a3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37223998"
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
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|""|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[[資料庫]](database-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 `DbStorageLocation`資料庫屬性必須設現有的 UNC 資料夾路徑或空字串。 空字串是預設的伺服器資料夾。 如果這個資料夾不存在，當您執行 `Create`、`Attach` 或 `Alter` 命令時，就會引發錯誤。  
  
 颾魤 ㄛ`DbStorageLocation`資料庫屬性無法設定為指向伺服器資料夾或其任何子資料夾。 如果此位置指向伺服器資料夾或其中任何一個子資料夾，當您執行 `Create`、`Attach` 或 `Alter` 命令時，就會引發錯誤。  
  
## <a name="see-also"></a>另請參閱  
 <xref:Microsoft.AnalysisServices.Database.DbStorageLocation%2A>   
 [附加和卸離 Analysis Services 資料庫](../../multidimensional-models/attach-and-detach-analysis-services-databases.md)  
  
  
