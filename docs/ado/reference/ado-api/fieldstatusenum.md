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
ms.openlocfilehash: d3ad005a4c26a033f6c97d97def4cd55d867c14e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "67918661"
---
# <a name="fieldstatusenum"></a>FieldStatusEnum
指定[欄位物件](../../../ado/reference/ado-api/field-object.md)的[狀態](../../../ado/reference/ado-api/status-property-ado-field.md)。  
  
 **AdFieldPending\* **值表示導致狀態設定的作業，而且可能會與其他狀態值結合。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adFieldAlreadyExists**|26|表示指定的欄位已經存在。|  
|**adFieldBadStatus**|12|表示從 ADO 傳送到 OLE DB 提供者的狀態值無效。 可能的原因包括 OLE DB 1.0 或1.1 提供者，或[值](../../../ado/reference/ado-api/value-property-ado.md)和[狀態](../../../ado/reference/ado-api/status-property-ado-field.md)的不適當組合。|  
|**adFieldCannotComplete**|20|表示[來源](../../../ado/reference/ado-api/source-property-ado-record.md)所指定的 URL 伺服器無法完成作業。|  
|**adFieldCannotDeleteSource**|23|表示在移動作業期間，樹狀目錄或子樹已移至新位置，但無法刪除來源。|  
|**adFieldCantConvertValue**|2|表示無法抓取或儲存欄位，而不會遺失資料。|  
|**adFieldCantCreate**|7|指出無法加入欄位，因為提供者超過限制（例如允許的欄位數目）。|  
|**adFieldDataOverflow**|6|表示從提供者傳回的資料溢位欄位的資料類型。|  
|**adFieldDefault**|13|表示設定資料時，使用欄位的預設值。|  
|**adFieldDoesNotExist**|16|表示指定的欄位不存在。|  
|**adFieldIgnore**|15|表示在設定來源中的資料值時，略過此欄位。 提供者未設定任何值。|  
|**adFieldIntegrityViolation**|10|表示欄位無法修改，因為它是計算或衍生的實體。|  
|**adFieldInvalidURL**|17|表示資料來源 URL 包含不正確字元。|  
|**adFieldIsNull**|3|指出提供者傳回 VT_Null 類型的 VARIANT 值，而且欄位不是空的。|  
|**adFieldOK**|0|預設值。 表示已成功加入或刪除欄位。|  
|**adFieldOutOfSpace**|22|指出提供者無法取得足夠的儲存空間來完成移動或複製操作。|  
|**adFieldPendingChange**|0x40000|表示已刪除欄位，然後再重新加入（可能使用不同的資料類型），或先前具有**adFieldOK**狀態的欄位值已變更。 欄位的最終形式會在呼叫[Update](../../../ado/reference/ado-api/update-method.md)方法之後修改[Fields](../../../ado/reference/ado-api/fields-collection-ado.md)集合。|  
|**adFieldPendingDelete**|0x20000|表示**刪除**作業導致狀態設定。 呼叫**Update**方法之後，欄位已從**Fields**集合中標示為要刪除。|  
|**adFieldPendingInsert**|0x10000|表示**附加**作業導致狀態設定。 在呼叫**Update**方法之後，**欄位**已標記為要加入至**Fields**集合。|  
|**adFieldPendingUnknown**|0x80000|指出提供者無法判斷哪一個作業導致欄位狀態設定。|  
|**adFieldPendingUnknownDelete**|0x100000|指出提供者無法判斷哪一個作業導致欄位狀態設定，以及在呼叫**Update**方法之後，欄位集合中將會**刪除該欄位**。|  
|**adFieldPermissionDenied**|9|表示欄位無法修改，因為它是定義為唯讀。|  
|**adFieldReadOnly**|24|表示資料來源中的欄位定義為唯讀。|  
|**adFieldResourceExists**|19|指出提供者無法執行作業，因為物件已存在於目的地 URL，而且無法覆寫物件。|  
|**adFieldResourceLocked**|18|指出提供者無法執行作業，因為資料來源已被一或多個其他應用程式或進程鎖定。|  
|**adFieldResourceOutOfScope**|25|表示來源或目的地 URL 超出目前記錄的範圍。|  
|**adFieldSchemaViolation**|11|表示此值違反了欄位的資料來源架構條件約束。|  
|**adFieldSignMismatch**|5|表示提供者所傳回的資料值已簽署，但 ADO 域值的資料類型不帶正負號。|  
|**adFieldTruncated**|4|表示從資料來源讀取時，已截斷可變長度的資料。|  
|**adFieldUnavailable**|8|表示在讀取資料來源時，提供者無法判斷值。 例如，剛建立資料列，資料行的預設值無法使用，而且尚未指定新的值。|  
|**adFieldVolumeNotFound**|21|指出提供者找不到 URL 所指示的存放磁片區。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等  
 這些常數沒有 ADO/WFC 對應項。  
  
## <a name="applies-to"></a>套用至  
 [Status 屬性 (ADO Field)](../../../ado/reference/ado-api/status-property-ado-field.md)
