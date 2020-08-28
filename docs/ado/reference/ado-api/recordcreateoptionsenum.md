---
description: RecordCreateOptionsEnum
title: RecordCreateOptionsEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RecordCreateOptionsEnum
helpviewer_keywords:
- RecordCreateOptionsEnum enumeration [ADO]
ms.assetid: 6d746670-0850-4065-9cd4-168dea1d3ea9
author: rothja
ms.author: jroth
ms.openlocfilehash: 4393196078b7800e1f1ec324c612918d7b8380e9
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989819"
---
# <a name="recordcreateoptionsenum"></a>RecordCreateOptionsEnum
指定是否應該開啟現有的**記錄**，或針對[Record](./record-object-ado.md)物件[Open](./open-method-ado-record.md)方法建立的新**記錄**。 這些值可以與 AND 運算子合併。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adCreateCollection**|0x2000|在*來源*參數指定的節點上建立新的**記錄**，而不是開啟現有的**記錄**。 如果來源指向現有的節點，則會發生執行階段錯誤，除非 **adCreateCollection** 結合 **adOpenIfExists** 或 **adCreateOverwrite**。|  
|**adCreateNonCollection**|0|建立[adSimpleRecord](./recordtypeenum.md)類型的新**記錄**。|  
|**adCreateOverwrite**|0x4000000|修改建立旗標 **adCreateCollection**、 **adCreateNonCollection**和 **adCreateStructDoc**。 當或搭配此值和其中一個建立旗標值使用時，如果來源 URL 指向現有的節點或 **記錄**，則會覆寫現有的記錄，並在其位置建立新的 **記錄** 。 此值不能與 **adOpenIfExists**一起使用。|  
|**adCreateStructDoc**|0x80000000|建立[adStructDoc](./recordtypeenum.md)類型的新**記錄**，而不是開啟現有的**記錄**。|  
|**adFailIfNotExists**|-1|預設值。 如果 *來源* 指向不存在的節點，則會導致執行階段錯誤。|  
|**adOpenIfExists**|0x2000000|修改建立旗標 **adCreateCollection**、 **adCreateNonCollection**和 **adCreateStructDoc**。 當或搭配此值和其中一個建立旗標值使用時，如果來源 URL 指向現有的節點或 **記錄** 物件，則提供者必須開啟現有的記錄，而不是建立新的 **記錄** 。 此值不能與 **adCreateOverwrite**一起使用。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 這些常數沒有 ADO/WFC 對等專案。  
  
## <a name="applies-to"></a>套用至  
 [Open 方法 (ADO Record)](./open-method-ado-record.md)