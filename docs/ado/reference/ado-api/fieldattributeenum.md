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
manager: craigg
ms.openlocfilehash: 80fb27aa51d6e0a44f8f006711708e24cd04bef3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47632316"
---
# <a name="fieldattributeenum"></a>FieldAttributeEnum
指定一或多個屬性[欄位](../../../ado/reference/ado-api/field-object.md)物件。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adFldCacheDeferred**|0x1000|表示提供者會快取欄位值，而且後續的讀取已從快取。|  
|**adFldFixed**|0x10|表示欄位包含固定長度的資料。|  
|**adFldIsChapter**|0x2000|表示欄位包含章節的值，指定與此父欄位相關的特定子資料錄集。 通常用於一章欄位與資料成形或篩選。|  
|**adFldIsCollection**|0x40000|指出欄位會指定記錄所表示的資源是其他資源，例如資料夾，而不是簡單的資源，例如文字檔案的集合。|  
|**adFldKeyColumn**|0x8000|指出欄位指定全部或一部分資料行的主索引鍵。|  
|**adFldIsDefaultStream**|0x20000|表示欄位包含預設資料流記錄所表示的資源。 例如，預設資料流可以是 HTML 內容的網站，自動會在指定的根 URL 時所提供的根資料夾。|  
|**adFldIsNullable**|0x20|表示欄位可接受 null 值。|  
|**adFldIsRowURL**|0x10000|表示欄位包含之 URL 的名稱來自記錄所代表的資料存放區的資源。|  
|**adFldLong**|0x80|表示欄位是長的二進位欄位。 也會指出，您可以使用[AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md)並[GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md)方法。|  
|**adFldMayBeNull**|0x40|表示您可以從欄位讀取 null 值。|  
|**adFldMayDefer**|0x2|表示欄位會延後 — 也就是欄位的值不會擷取從資料來源與整個記錄，但只有在您明確地存取時。|  
|**adFldNegativeScale**|0x4000|表示欄位代表一個數字值，從支援負的小數位數值的資料行。 指定標尺[NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md)屬性。|  
|**adFldRowID**|0x100|表示欄位包含不能寫入，且具有無意義的值，但若要識別 （例如記錄編號、 唯一識別碼和其他等等） 的資料列的永續性資料列識別碼。|  
|**adFldRowVersion**|0x200|表示欄位包含某種用來追蹤更新的日期或時間戳記。|  
|**adFldUnknownUpdatable**|0x8|指出提供者無法判斷您可以寫入的欄位。|  
|**adFldUnspecified**|-1 0xFFFFFFFF|指出提供者未指定欄位的欄位屬性。|  
|**adFldUpdatable**|0x4|表示您可以寫入的欄位。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 封裝： **com.ms.wfc.data**  
  
|常數|  
|--------------|  
|AdoEnums.FieldAttribute.CACHEDEFERRED|  
|AdoEnums.FieldAttribute.FIXED|  
|AdoEnums.FieldAttribute.ISNULLABLE|  
|AdoEnums.FieldAttribute.LONG|  
|AdoEnums.FieldAttribute.MAYBENULL|  
|AdoEnums.FieldAttribute.MAYDEFER|  
|AdoEnums.FieldAttribute.NEGATIVESCALE|  
|AdoEnums.FieldAttribute.ROWID|  
|AdoEnums.FieldAttribute.ROWVERSION|  
|AdoEnums.FieldAttribute.UNKNOWNUPDATABLE|  
|AdoEnums.FieldAttribute.UNSPECIFIED|  
|AdoEnums.FieldAttribute.UPDATABLE|  
  
## <a name="applies-to"></a>適用於  
  
|||  
|-|-|  
|[Append 方法 (ADO)](../../../ado/reference/ado-api/append-method-ado.md)|[Attributes 屬性 (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)|
