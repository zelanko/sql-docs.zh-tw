---
title: Password 元素 (XMLA) |Microsoft Docs
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
- Password Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Password
- urn:schemas-microsoft-com:xml-analysis#Password
- microsoft.xml.analysis.password
helpviewer_keywords:
- Password element
ms.assetid: 8a0603bd-f6a1-4b86-84f1-c83d0b03951b
caps.latest.revision: 11
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9ab15627b4f5cde95ecff8f368d294d4336060cc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37328448"
---
# <a name="password-element-xmla"></a>Password 元素 (XMLA)
  決定父元素所要使用的密碼[備份](../xml-elements-commands/backup-element-xmla.md)或是[還原](../xml-elements-commands/restore-element-xmla.md)命令用於加密或解密備份檔案。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Backup> <!-- or Restore -->  
   ...  
   <Password>...</Password>  
   ...  
</Backup>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[備份](../xml-elements-commands/backup-element-xmla.md)，[還原](../xml-elements-commands/restore-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 若為 `Backup` 命令，如果沒有包含 `Password` 元素或者它包含空字串，系統就不會加密備份檔案。  
  
 若為 `Restore` 命令，如果沒有包含 `Password` 元素或者它包含空字串，則在嘗試還原加密的備份檔案時，就會發生錯誤。  
  
 如果 `Location` 元素包含在 `Backup` 或 `Restore` 命令中，系統就會針對備份和遠端備份檔案使用相同的 `Password` 元素。 如需有關遠端備份檔案的詳細資訊，請參閱 <<c0> [ 備份、 還原和同步處理資料庫&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)。</c0>  
  
## <a name="see-also"></a>另請參閱  
 [Location 項目&#40;XMLA&#41;](location-element-xmla.md)   
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
