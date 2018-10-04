---
title: AllowOverwrite 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- AllowOverwrite Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.allowoverwrite
- urn:schemas-microsoft-com:xml-analysis#EndSession
helpviewer_keywords:
- AllowOverwrite element
ms.assetid: e7e92481-5f29-47f2-9efd-4e5e60c002bb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: eb0d58570349fbbb17b442ddebc0fd3193531149
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48131428"
---
# <a name="allowoverwrite-element-xmla"></a>AllowOverwrite 元素 (XMLA)
  決定是否父系[備份](../xml-elements-commands/backup-element-xmla.md)或是[還原](../xml-elements-commands/restore-element-xmla.md)命令嘗試覆寫目標檔案或資料庫。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Backup> <!-- or Restore -->  
   ...  
   <AllowOverwrite>...</AllowOverwrite>  
   ...  
</Backup>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|布林|  
|預設值|False|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[備份](../xml-elements-commands/backup-element-xmla.md)，[還原](../xml-elements-commands/restore-element-xmla.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 若為 `Backup` 命令，`AllowOverwrite` 元素會決定此命令是否可覆寫 `File` 元素中指定的備份檔案。  
  
 針對`Restore`項目，`AllowOverwrite`元素會決定此命令是否可以覆寫[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中所指定資料庫`DatabaseName`項目。  
  
## <a name="see-also"></a>另請參閱  
 [DatabaseName 元素&#40;XMLA&#41;](name-element-xmla.md)   
 [檔案項目&#40;XMLA&#41;](file-element-xmla.md)   
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
