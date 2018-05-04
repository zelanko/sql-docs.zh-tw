---
title: RecordCreateOptionsEnum |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RecordCreateOptionsEnum
helpviewer_keywords:
- RecordCreateOptionsEnum enumeration [ADO]
ms.assetid: 6d746670-0850-4065-9cd4-168dea1d3ea9
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3109e7e7116fac22e007c65167bb718edf2b29b7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="recordcreateoptionsenum"></a>RecordCreateOptionsEnum
指定是否將現有**記錄**應該開啟或新**記錄**建立[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件[開啟](../../../ado/reference/ado-api/open-method-ado-record.md)方法。 值可以與 AND 運算子結合。  
  
|常數|Value|Description|  
|--------------|-----------|-----------------|  
|**adCreateCollection**|0x2000|建立新**記錄**所指定的節點在*來源*參數，而不是開啟的現有**記錄**。 如果來源會指向現有的節點，則會發生執行階段錯誤，除非**adCreateCollection**結合**adOpenIfExists**或**adCreateOverwrite**。|  
|**adCreateNonCollection**|0|建立新**記錄**型別的[adSimpleRecord](../../../ado/reference/ado-api/recordtypeenum.md)。|  
|**adCreateOverwrite**|0x4000000|修改建立旗標**adCreateCollection**， **adCreateNonCollection**，和**adCreateStructDoc**。 當使用此值，其中一個建立旗標值，如果來源 URL 指向現有的節點或**記錄**，則現有**記錄**不覆寫在其位置建立新。 此值不能搭配**adOpenIfExists**。|  
|**adCreateStructDoc**|0x80000000|建立新**記錄**型別的[adStructDoc](../../../ado/reference/ado-api/recordtypeenum.md)，而不是開啟的現有**記錄**。|  
|**adFailIfNotExists**|-1|預設值。 如果會導致執行階段錯誤*來源*指向不存在的節點。|  
|**adOpenIfExists**|0x2000000|修改建立旗標**adCreateCollection**， **adCreateNonCollection**，和**adCreateStructDoc**。 當使用此值，其中一個建立旗標值，如果來源 URL 指向現有的節點或**記錄**物件，然後提供者必須開啟現有**記錄**而不是建立新的其中一個。 此值不能搭配**adCreateOverwrite**。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 這些常數沒有 ADO/WFC 對等項目。  
  
## <a name="applies-to"></a>適用於  
 [Open 方法 (ADO Record)](../../../ado/reference/ado-api/open-method-ado-record.md)
