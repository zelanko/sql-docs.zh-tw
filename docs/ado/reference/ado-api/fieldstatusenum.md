---
title: "FieldStatusEnum |Microsoft 文件"
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
- FieldStatusEnum
helpviewer_keywords:
- FieldStatusEnum enumeration [ADO]
ms.assetid: e06da1e2-303f-41b2-a3b0-61e233da152c
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 33ea3379808e818b1afd723ce9223858896ea709
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="fieldstatusenum"></a>FieldStatusEnum
指定[狀態](../../../ado/reference/ado-api/status-property-ado-field.md)的[欄位物件](../../../ado/reference/ado-api/field-object.md)。  
  
 **AdFieldPending\* **值表示作業導致的狀態設定，可能會與其他狀態的值結合。  
  
|常數|值|Description|  
|--------------|-----------|-----------------|  
|**adFieldAlreadyExists**|26|指出指定的欄位已經存在。|  
|**adFieldBadStatus**|12|表示無效的狀態值，OLE DB 提供者從 ADO 傳送。 可能的原因包括 OLE DB 1.0 或 1.1 版的提供者或使用不正確的組合[值](../../../ado/reference/ado-api/value-property-ado.md)和[狀態](../../../ado/reference/ado-api/status-property-ado-field.md)。|  
|**adFieldCannotComplete**|20|指出所指定的伺服器 URL 的[來源](../../../ado/reference/ado-api/source-property-ado-record.md)無法完成作業。|  
|**adFieldCannotDeleteSource**|23|表示在移動作業時，樹狀目錄或樹狀子目錄已移至新位置，但無法刪除來源。|  
|**adFieldCantConvertValue**|2|表示無法擷取的欄位，或儲存而不會遺失資料。|  
|**adFieldCantCreate**|7|指出因為提供者已超過限制 （例如欄位數目），不可以加入欄位。|  
|**adFieldDataOverflow**|6|指出提供者所傳回的資料造成溢位欄位的資料類型。|  
|**adFieldDefault**|13|表示欄位的預設值已設定資料時使用。|  
|**adFieldDoesNotExist**|16|指出指定的欄位不存在。|  
|**adFieldIgnore**|15|表示，在來源中的設定資料值時，已略過此欄位。 提供者會將任何值。|  
|**adFieldIntegrityViolation**|10|表示無法修改的欄位，因為它是導出或衍生的實體。|  
|**adFieldInvalidURL**|17|表示資料來源 URL 包含無效的字元。|  
|**adFieldIsNull**|3|指出提供者傳回 VT_NULL 型別的變數值和欄位不是空白。|  
|**adFieldOK**|0|預設值。 表示已成功加入或刪除欄位。|  
|**adFieldOutOfSpace**|22|表示提供者無法取得足夠的儲存空間可完成移動或複製作業。|  
|**adFieldPendingChange**|0x40000|表示欄位已經刪除而且又重新加入，可能是不同的資料類型，或其先前狀態的欄位值的**adFieldOK**已變更。 將修改的欄位的最終格式[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)後的集合[更新](../../../ado/reference/ado-api/update-method.md)方法呼叫。|  
|**adFieldPendingDelete**|0x20000|表示**刪除**作業造成要設定的狀態。 欄位已標示為刪除**欄位**後的集合**更新**方法呼叫。|  
|**adFieldPendingInsert**|0x10000|表示**附加**作業造成要設定的狀態。 **欄位**已標示為要加入至**欄位**後的集合**更新**方法呼叫。|  
|**adFieldPendingUnknown**|0x80000|指出提供者無法決定要設定哪些作業導致欄位狀態。|  
|**adFieldPendingUnknownDelete**|0x100000|指出提供者無法決定哪一個作業造成要設定的欄位狀態和刪除欄位，從**欄位**後的集合**更新**方法呼叫。|  
|**adFieldPermissionDenied**|9|表示無法修改的欄位，因為它定義為唯讀。|  
|**adFieldReadOnly**|24|表示資料來源中的欄位會定義為唯讀。|  
|**adFieldResourceExists**|19|表示提供者無法執行作業，因為物件已經存在於目的地 URL，並不能覆寫該物件。|  
|**adFieldResourceLocked**|18|表示提供者無法執行作業，因為資料來源已鎖定一或多個其他應用程式或程序。|  
|**adFieldResourceOutOfScope**|25|表示目前資料錄的範圍外的來源或目的地 URL。|  
|**adFieldSchemaViolation**|11|表示的值違反資料欄位的資料來源結構描述條件約束。|  
|**adFieldSignMismatch**|5|表示提供者傳回的資料值為 signed，但 ADO 欄位值的資料型別為 unsigned。|  
|**adFieldTruncated**|4|表示從資料來源讀取時，已截斷可變長度的資料。|  
|**adFieldUnavailable**|8|指出提供者可能無法決定值從資料來源讀取時。 例如，剛建立的資料列、 資料行的預設值無法使用，和尚未從未指定新的值。|  
|**adFieldVolumeNotFound**|21|表示提供者找不到安全的 URL 的存放磁碟區。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 這些常數沒有 ADO/WFC 對等項目。  
  
## <a name="applies-to"></a>適用於  
 [Status 屬性 （ADO 欄位）](../../../ado/reference/ado-api/status-property-ado-field.md)

