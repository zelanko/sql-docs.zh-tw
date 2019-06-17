---
title: DatabaseToConnect 元素 (DTA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- DatabaseToConnect element
ms.assetid: 65153a66-3aee-4429-99b7-0816ac23c285
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4fef2df598d96b33def41f27345f88226fd4c6b5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63185420"
---
# <a name="databasetoconnect-element-dta"></a>DatabaseToConnect 元素 (DTA)
  指定微調工作負載時，Database Engine Tuning Advisor 所連接的第一個資料庫。  
  
## <a name="syntax"></a>語法  
  
```  
  
    <TuningOptions>  
...code removed here...  
      <DatabaseToConnect>...</DatabaseToConnect>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|**資料類型和長度**|`string`，沒有長度限制。|  
|**預設值**|無。|  
|**出現次數**|選擇性。 每個 `TuningOptions` 元素可以使用這個元素一次。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[TuningOptions 元素 &#40;DTA&#41;](tuningoptions-element-dta.md)|  
|**子元素**|None|  
  
## <a name="remarks"></a>備註  
 請利用 `DatabaseToConnect` 來指定 Database Engine Tuning Advisor 開始微調工作階段時，所要連接的第一個資料庫的名稱。 您只能利用這個元素來指定一個資料庫。 如果指定了多個資料庫名稱，Database Engine Tuning Advisor 就會傳回錯誤。  
  
## <a name="example"></a>範例  
 如需使用範例，請參閱[含內嵌工作負載的 XML 輸入檔範例 &#40;DTA&#41;](xml-input-file-sample-with-inline-workload-dta.md)。  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入檔參考XML Input File ReferenceDatabase Engine Tuning Advisor&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
