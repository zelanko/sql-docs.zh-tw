---
title: AllowNullsEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- AllowNullsEnum
helpviewer_keywords:
- AllowNullsEnum enumeration [ADOX]
ms.assetid: 6acf3689-1a7f-4379-9d7f-df452ccbac27
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9d1f4f5ce302c6f9e3e28b037c838d452f771114
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47692686"
---
# <a name="allownullsenum"></a>AllowNullsEnum
指定具有 null 值的記錄都編製索引。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adIndexNullsAllow**|0|索引，並讓項目索引鍵資料行是 null。 如果索引鍵資料行中輸入 null 值，則此項目會插入索引中。|  
|**adIndexNullsDisallow**|1|預設值。 索引不允許索引鍵資料行是 null 的項目。 如果索引鍵資料行中輸入 null 值，則會發生錯誤。|  
|**adIndexNullsIgnore**|2|索引不會插入包含 null 的索引鍵的項目。 如果索引鍵資料行中輸入 null 值，則會忽略項目，並不會發生錯誤。|  
|**adIndexNullsIgnoreAny**|4|索引不會插入其中某些索引鍵資料行具有 null 值的項目。 具有多重資料行索引的索引鍵，如果在某個資料行中，輸入 null 值的項目會被忽略，不會發生錯誤。|  
  
## <a name="applies-to"></a>適用於  
 [IndexNulls 屬性 (ADOX)](../../../ado/reference/adox-api/indexnulls-property-adox.md)
