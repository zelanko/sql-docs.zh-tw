---
title: ConnectionString 元素 (XMLA) |Microsoft 文件
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
- ConnectionString Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.connectionstring
- urn:schemas-microsoft-com:xml-analysis#ConnectionString
- http://schemas.microsoft.com/analysisservices/2003/engine#ConnectionString
helpviewer_keywords:
- ConnectionString element
ms.assetid: 3b0575aa-79ed-4f14-ae7e-dd587af4cdb1
caps.latest.revision: 13
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 12d69bfe2b8dc8bda91bc873167bb3208203d728
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36023868"
---
# <a name="connectionstring-element-xmla"></a>ConnectionString 元素 (XMLA)
  包含父系所使用的連接字串[位置](location-element-xmla.md)或[來源](source-element-xmla.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Location> <!-- or Source -->  
   ...  
   <ConnectionString>...</ConnectionString>  
   ...  
</Location>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|無|  
|基數為上階或父系|基數|  
|[位置](location-element-xmla.md)|1-1：只出現一次的必要元素。|  
|[Source](source-element-xmla.md)|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[位置](location-element-xmla.md)，[來源](source-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 若為 `Location` 元素，`ConnectionString` 元素會包含 `Restore` 或 `Synchronize` 命令用來更新本機資料來源或連接至遠端執行個體的連接字串。  
  
 若為 `Source` 元素，`ConnectionString` 元素會包含 `Synchronize` 命令用來連接至來源執行個體的連接字串。  
  
 如需有關備份和還原物件的詳細資訊，請參閱[備份、 還原及同步處理資料庫&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Restore 元素&#40;XMLA&#41;](../xml-elements-commands/restore-element-xmla.md)   
 [同步處理項目&#40;XMLA&#41;](../xml-elements-commands/synchronize-element-xmla.md)   
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  