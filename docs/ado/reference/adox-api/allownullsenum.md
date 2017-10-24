---
title: "AllowNullsEnum |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- AllowNullsEnum
helpviewer_keywords:
- AllowNullsEnum enumeration [ADOX]
ms.assetid: 6acf3689-1a7f-4379-9d7f-df452ccbac27
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2b9bb610e1b3f4a31e29ddee31e569c34528e243
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="allownullsenum"></a>AllowNullsEnum
指定具有 null 值的記錄都編製索引。  
  
|常數|值|Description|  
|--------------|-----------|-----------------|  
|**adIndexNullsAllow**|0|索引，並讓項目索引鍵資料行是 null。 如果索引鍵資料行中輸入 null 值，則會將項目插入至索引。|  
|**adIndexNullsDisallow**|1|預設值。 索引不允許項目索引鍵資料行是 null。 如果索引鍵資料行中輸入 null 值，則會發生錯誤。|  
|**adIndexNullsIgnore**|2|索引不會插入包含 null 索引鍵的項目。 如果索引鍵資料行中輸入 null 值，則會忽略項目，並不會發生錯誤。|  
|**adIndexNullsIgnoreAny**|4|索引不會插入其中某些索引鍵資料行有 null 值的項目。 具有多個資料行索引的索引鍵，如果某些資料行中，輸入 null 值項目會被忽略，不會發生錯誤。|  
  
## <a name="applies-to"></a>適用於  
 [IndexNulls 屬性 (ADOX)](../../../ado/reference/adox-api/indexnulls-property-adox.md)

