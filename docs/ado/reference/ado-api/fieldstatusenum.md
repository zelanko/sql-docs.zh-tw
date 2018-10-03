---
title: FieldStatusEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FieldStatusEnum
helpviewer_keywords:
- FieldStatusEnum enumeration [ADO]
ms.assetid: e06da1e2-303f-41b2-a3b0-61e233da152c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4e2f08868aa581136bc155011671e0b8b1c55e68
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47606670"
---
# <a name="fieldstatusenum"></a>FieldStatusEnum
指定[狀態](../../../ado/reference/ado-api/status-property-ado-field.md)的[Field 物件](../../../ado/reference/ado-api/field-object.md)。  
  
 **AdFieldPending\*** 值會指出的作業，導致狀態，以進行設定，並可能會與其他狀態的值結合。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adFieldAlreadyExists**|26|表示指定的欄位已存在。|  
|**adFieldBadStatus**|12|表示無效的狀態值已傳送從 ADO 的 OLE DB 提供者。 可能的原因包括 OLE DB 1.0 或 1.1 版的提供者或使用不正確的組合[值](../../../ado/reference/ado-api/value-property-ado.md)並[狀態](../../../ado/reference/ado-api/status-property-ado-field.md)。|  
|**adFieldCannotComplete**|20|指出所指定的伺服器 URL[來源](../../../ado/reference/ado-api/source-property-ado-record.md)無法完成作業。|  
|**adFieldCannotDeleteSource**|23|表示移動作業時，樹狀目錄或樹狀子目錄已移至新的位置，但無法刪除來源。|  
|**adFieldCantConvertValue**|2|表示欄位無法擷取或儲存而不會遺失資料。|  
|**adFieldCantCreate**|7|指出因為提供者已超過限制 （例如允許的欄位數目），不可能加入的欄位。|  
|**adFieldDataOverflow**|6|指出提供者傳回的資料造成溢位 欄位的資料類型。|  
|**adFieldDefault**|13|表示欄位的預設值已設定資料時使用。|  
|**adFieldDoesNotExist**|16|指出指定的欄位不存在。|  
|**adFieldIgnore**|15|表示這個欄位已略過，當設定資料來源中的值。 提供者會將任何值。|  
|**adFieldIntegrityViolation**|10|表示無法修改欄位，因為它是導出或衍生的實體。|  
|**adFieldInvalidURL**|17|表示資料來源 URL 包含無效的字元。|  
|**adFieldIsNull**|3|表示的提供者傳回型別 VT_NULL VARIANT 值，而且該欄位不是空白。|  
|**adFieldOK**|0|預設值。 表示已成功新增或刪除欄位。|  
|**adFieldOutOfSpace**|22|表示提供者無法取得足夠的儲存空間可完成的移動或複製作業。|  
|**adFieldPendingChange**|0x40000|表示已刪除並再重新加入，可能是不同的資料類型，或欄位的先前狀態的欄位值的**adFieldOK**已變更。 將修改欄位的最終形式[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)集合之後[更新](../../../ado/reference/ado-api/update-method.md)呼叫方法。|  
|**adFieldPendingDelete**|0x20000|指出**刪除**作業會導致要設定的狀態。 欄位已標示為要刪除**欄位**集合之後,**更新**呼叫方法。|  
|**adFieldPendingInsert**|0x10000|指出**Append**作業會導致要設定的狀態。 **欄位**已標示要加入至**欄位**後的集合**Update**呼叫方法。|  
|**adFieldPendingUnknown**|0x80000|指出提供者無法判斷何種作業導致欄位狀態中設定。|  
|**adFieldPendingUnknownDelete**|0x100000|指出提供者無法判斷哪一個作業造成欄位狀態來設定，並刪除欄位，從**欄位**集合之後,**更新**呼叫方法。|  
|**adFieldPermissionDenied**|9|表示無法修改欄位，因為它定義為唯讀。|  
|**adFieldReadOnly**|24|表示資料來源中的欄位定義為唯讀。|  
|**adFieldResourceExists**|19|表示提供者無法執行作業，因為物件已經存在於目的地 URL，而且不能覆寫的物件。|  
|**adFieldResourceLocked**|18|表示提供者無法執行作業，因為資料來源已被鎖定一或多個其他應用程式或程序。|  
|**adFieldResourceOutOfScope**|25|表示目前資料錄範圍以外的來源或目的地 URL。|  
|**adFieldSchemaViolation**|11|表示的值違反資料欄位的資料來源結構描述條件約束。|  
|**adFieldSignMismatch**|5|表示提供者傳回的資料值已簽署，但 ADO 欄位值的資料類型是不帶正負號。|  
|**adFieldTruncated**|4|表示從資料來源讀取時，已截斷可變長度的資料。|  
|**adFieldUnavailable**|8|指出提供者可能未決定的值從資料來源讀取時。 比方說，剛建立的資料列、 資料行的預設值無法使用，及尚未從未指定新的值。|  
|**adFieldVolumeNotFound**|21|表示找不到 URL 所指示的儲存體磁碟區提供者。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 這些常數不需要 ADO/WFC 對等項目。  
  
## <a name="applies-to"></a>適用於  
 [Status 屬性 (ADO Field)](../../../ado/reference/ado-api/status-property-ado-field.md)
