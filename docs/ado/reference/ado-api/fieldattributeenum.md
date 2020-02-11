---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0d375ed3dd4ea7ae7e2e5405d1feec962c5f56ae
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67918707"
---
# <a name="fieldattributeenum"></a>FieldAttributeEnum
指定[欄位](../../../ado/reference/ado-api/field-object.md)物件的一或多個屬性。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adFldCacheDeferred**|0x1000|指出提供者會快取域值，並從快取中完成後續讀取。|  
|**adFldFixed**|0x10|指出欄位包含固定長度的資料。|  
|**adFldIsChapter**|0x2000|指出此欄位包含章節值，其指定與此父欄位相關的特定子記錄集。 [章節] 欄位通常用於資料成形或篩選。|  
|**adFldIsCollection**|0x40000|表示欄位指定記錄所代表的資源是其他資源（例如資料夾）的集合，而不是簡單的資源，例如文字檔。|  
|**adFldKeyColumn**|0x8000|表示欄位會指定資料行的全部或部分主要索引鍵。|  
|**adFldIsDefaultStream**|0x20000|指出此欄位包含記錄所代表之資源的預設資料流程。 例如，預設資料流程可以是網站上根資料夾的 HTML 內容，當指定根 URL 時，它會自動提供服務。|  
|**adFldIsNullable**|0x20|表示欄位接受 null 值。|  
|**adFldIsRowURL**|0x10000|指出此欄位包含的 URL 會將資源命名為記錄所代表的資料存放區。|  
|**adFldLong**|0x80|表示欄位是長二進位欄位。 也表示您可以使用[AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md)和[GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md)方法。|  
|**adFldMayBeNull**|0x40|表示您可以從欄位讀取 null 值。|  
|**adFldMayDefer**|0x2|表示欄位已延後（也就是，系統不會使用整筆記錄從資料來源中抓取域值，但只有在您明確存取時）。|  
|**adFldNegativeScale**|0x4000|表示欄位代表來自支援負值小數值之資料行的數值。 小數值是由[NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md)屬性所指定。|  
|**adFldRowID**|0x100|指出欄位包含無法寫入的持續性資料列識別碼，而且沒有任何有意義的值，除非識別資料列（例如記錄號碼、唯一識別碼等等）。|  
|**adFldRowVersion**|0x200|指出欄位包含用來追蹤更新的某種時間或日期戳記。|  
|**adFldUnknownUpdatable**|0x8|指出提供者無法判斷您是否可以寫入欄位。|  
|**adFldUnspecified**|-1 0xFFFFFFFF|指出提供者未指定欄位屬性。|  
|**adFldUpdatable**|0x4|表示您可以寫入欄位。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等  
 Package： **.com. wfc. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums.FieldAttribute.CACHEDEFERRED|  
|AdoEnums. FieldAttribute. FIXED|  
|AdoEnums. FieldAttribute. ISNullABLE|  
|AdoEnums. FieldAttribute. LONG|  
|AdoEnums.FieldAttribute.MAYBENull|  
|AdoEnums.FieldAttribute.MAYDEFER|  
|AdoEnums.FieldAttribute.NEGATIVESCALE|  
|AdoEnums. FieldAttribute. ROWID|  
|AdoEnums. FieldAttribute. ROWVERSION|  
|AdoEnums.FieldAttribute.UNKNOWNUPDATABLE|  
|AdoEnums. FieldAttribute。未指定|  
|AdoEnums. FieldAttribute. 可更新|  
  
## <a name="applies-to"></a>套用至  
  
|||  
|-|-|  
|[Append 方法 (ADO)](../../../ado/reference/ado-api/append-method-ado.md)|[Attributes 屬性 (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)|
