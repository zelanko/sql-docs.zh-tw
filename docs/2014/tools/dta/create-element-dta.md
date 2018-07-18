---
title: Create 元素 (DTA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Create element (DTA)
ms.assetid: 9d076c90-f933-45f4-b6d9-447793f6528b
caps.latest.revision: 12
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 33bb86a6c677affb8301d836a254284749a17fbc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37317378"
---
# <a name="create-element-dta"></a>Create 元素 (DTA)
  包含使用者指定組態中之索引、統計資料或堆積結構的相關資訊。  
  
## <a name="syntax"></a>語法  
  
```  
  
<Recommendation>  
    <Create>  
    ...code removed here...  
    </Create>  
</Recommendation>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|**資料類型和長度**|無。|  
|**預設值**|無。|  
|**出現次數**|每個實體設計結構類型 (索引、統計資料或堆積結構) 都需要使用這個元素一次。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[Recommendation 元素&#40;DTA&#41;](recommendation-element-dta.md)|  
|**子元素**|[編製索引的項目&#40;DTA&#41;](index-element-dta.md)<br /><br /> `Statistics` 項目 (請參閱[Database Engine Tuning Advisor XML 結構描述](http://schemas.microsoft.com/sqlserver/)資訊)<br /><br /> `Heap` 項目 (請參閱[Database Engine Tuning Advisor XML 結構描述](http://schemas.microsoft.com/sqlserver/)資訊)|  
  
## <a name="remarks"></a>備註  
 在 Database Engine Tuning Advisor XML 結構描述中，這個元素的名稱為 **CreateTypecomplexType** 。 它用來建立使用者指定組態的索引、統計資料和堆積結構。 請勿混淆這個 `Create` 元素與可用來建立檢視 (`CreateViewType`) 或資料分割 (`CreatePType`) 的其他類型。 請參閱[Database Engine Tuning Advisor XML 結構描述](http://schemas.microsoft.com/sqlserver/)如需其他資訊`Create`項目型別。  
  
## <a name="example"></a>範例  
 如需此元素的使用範例，請參閱[含使用者指定組態的 XML 輸入檔範例 &#40;DTA&#41;](xml-input-file-sample-with-user-specified-configuration-dta.md)。  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入檔參考 &#40;Database Engine Tuning Advisor&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
