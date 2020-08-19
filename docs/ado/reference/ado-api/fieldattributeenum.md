---
description: FieldAttributeEnum
title: FieldAttributeEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FieldAttributeEnum
helpviewer_keywords:
- FieldAttributeEnum enumeration [ADO]
ms.assetid: 6e34d886-005a-40dc-bd5c-6adcbf81e5cd
author: rothja
ms.author: jroth
ms.openlocfilehash: fd8910f07b5f30170e8addd90fa41ab3299fbda5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443760"
---
# <a name="fieldattributeenum"></a>FieldAttributeEnum
指定 [欄位](../../../ado/reference/ado-api/field-object.md) 物件的一或多個屬性。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adFldCacheDeferred**|0x1000|指出提供者會快取域值，並從快取中完成後續讀取。|  
|**adFldFixed**|0x10|表示欄位包含固定長度的資料。|  
|**adFldIsChapter**|0x2000|表示欄位包含章節值，此值會指定與此父欄位相關的特定子記錄集。 通常章節欄位會搭配資料成形或篩選使用。|  
|**adFldIsCollection**|0x40000|指出此欄位指定記錄所表示的資源是其他資源（例如資料夾）的集合，而不是簡單的資源，例如文字檔。|  
|**adFldKeyColumn**|0x8000|表示欄位會指定資料行的全部或一部分的主鍵。|  
|**adFldIsDefaultStream**|0x20000|表示欄位包含記錄所代表之資源的預設資料流程。 例如，預設的資料流程可以是網站根資料夾的 HTML 內容，當指定根 URL 時，系統就會自動提供此內容。|  
|**adFldIsNullable**|0x20|表示欄位接受 null 值。|  
|**adFldIsRowURL**|0x10000|指出此欄位包含的 URL 會從記錄所代表的資料存放區中，為資源命名。|  
|**adFldLong**|0x80|表示欄位是長二進位欄位。 也指出您可以使用 [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) 和 [GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md) 方法。|  
|**adFldMayBeNull**|0x40|指出您可以從欄位讀取 null 值。|  
|**adFldMayDefer**|0x2|表示欄位是延後的，也就是，不會從資料來源中取出整個記錄的域值，而只有在您明確存取這些欄位時。|  
|**adFldNegativeScale**|0x4000|表示欄位代表支援負小數值的資料行中的數值。 小數位數是由 [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md) 屬性所指定。|  
|**adFldRowID**|0x100|指出欄位包含無法寫入的持續性資料列識別碼，且除了識別資料列 (（例如記錄號碼、唯一) 識別碼等）之外，沒有任何有意義的值。|  
|**adFldRowVersion**|0x200|表示欄位包含某種用來追蹤更新的時間或日期戳記。|  
|**adFldUnknownUpdatable**|0x8|指出提供者無法判斷您是否可以寫入欄位。|  
|**adFldUnspecified**|-1 0xFFFFFFFF|表示提供者未指定欄位屬性。|  
|**adFldUpdatable**|0x4|指出您可以寫入欄位。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 封裝： **.com. 資料**  
  
|常數|  
|--------------|  
|AdoEnums.FieldAttribute.CACHEDEFERRED|  
|AdoEnums. FieldAttribute. FIXED|  
|AdoEnums. FieldAttribute. ISNullABLE|  
|AdoEnums. FieldAttribute. LONG|  
|AdoEnums. FieldAttribute. MAYBENull|  
|AdoEnums.FieldAttribute.MAYDEFER|  
|AdoEnums.FieldAttribute.NEGATIVESCALE|  
|AdoEnums. FieldAttribute|  
|AdoEnums. FieldAttribute. ROWVERSION|  
|AdoEnums.FieldAttribute.UNKNOWNUPDATABLE|  
|AdoEnums. FieldAttribute。未指定|  
|AdoEnums. FieldAttribute 可更新|  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [Append 方法 (ADO)](../../../ado/reference/ado-api/append-method-ado.md)  
    :::column-end:::
    :::column:::
        [Attributes 屬性 (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)  
    :::column-end:::
:::row-end:::
