---
title: Original 元素 (XMLA) |Microsoft 文件
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
- Original Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.original
- http://schemas.microsoft.com/analysisservices/2003/engine#Original
- urn:schemas-microsoft-com:xml-analysis#Original
helpviewer_keywords:
- Original element
ms.assetid: c98a3700-ac19-4341-85d9-5afedf662601
caps.latest.revision: 11
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 63ee76cd3b476b3a8dbf45a50ad0f9d22a55e0fb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36136483"
---
# <a name="original-element-xmla"></a>Original 元素 (XMLA)
  包含所使用的原始檔案系統儲存位置[資料夾](folder-element-xmla.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Folder>  
   ...  
   <Original>...</Original>  
   ...  
</Folder>  
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
|父元素|[資料夾](folder-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 `Original`元素包含 UNC 路徑的值以取代[新增](new-element-xmla.md)包含父代的項目`Folder`所有項目物件已還原或同步處理期間分別[還原](../xml-elements-commands/restore-element-xmla.md)或[Synchronize](../xml-elements-commands/synchronize-element-xmla.md)命令。 這個項目的值進行比較的值[StorageLocation](../../scripting/properties/storagelocation-element-assl.md)每個 cube、 量值群組或資料分割的項目，如果找到符合的值便`New`元素用來更新`StorageLocation`的在還原或同步處理期間的物件。  
  
 如需有關備份和還原物件的詳細資訊，請參閱[備份、 還原及同步處理資料庫&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  