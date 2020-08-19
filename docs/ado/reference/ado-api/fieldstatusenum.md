---
description: FieldStatusEnum
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 06044b54be7066deb5cf7510f060716106816805
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443710"
---
# <a name="fieldstatusenum"></a>FieldStatusEnum
指定[欄位物件](../../../ado/reference/ado-api/field-object.md)的[狀態](../../../ado/reference/ado-api/status-property-ado-field.md)。  
  
 **AdFieldPending \* **值表示導致狀態設定的作業，而且可能會與其他狀態值合併。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adFieldAlreadyExists**|26|指出指定的欄位已經存在。|  
|**adFieldBadStatus**|12|表示從 ADO 傳送到 OLE DB 提供者的狀態值無效。 可能的原因包括 OLE DB 1.0 或1.1 提供者，或 [值](../../../ado/reference/ado-api/value-property-ado.md) 和 [狀態](../../../ado/reference/ado-api/status-property-ado-field.md)的不當組合。|  
|**adFieldCannotComplete**|20|指出 [來源](../../../ado/reference/ado-api/source-property-ado-record.md) 所指定之 URL 的伺服器無法完成此作業。|  
|**adFieldCannotDeleteSource**|23|表示在移動作業期間，樹狀目錄或子樹已移至新位置，但無法刪除來源。|  
|**adFieldCantConvertValue**|2|表示無法在不遺失資料的情況下抓取或儲存欄位。|  
|**adFieldCantCreate**|7|表示無法加入欄位，因為提供者已超過限制 (例如允許的欄位數目) 。|  
|**adFieldDataOverflow**|6|指出從提供者傳回的資料會使欄位的資料類型溢位。|  
|**adFieldDefault**|13|指出設定資料時，會使用欄位的預設值。|  
|**adFieldDoesNotExist**|16|指出指定的欄位不存在。|  
|**adFieldIgnore**|15|指出當設定來源中的資料值時，已略過此欄位。 提供者未設定任何值。|  
|**adFieldIntegrityViolation**|10|表示欄位無法修改，因為它是計算或衍生的實體。|  
|**adFieldInvalidURL**|17|表示資料來源 URL 包含不正確字元。|  
|**adFieldIsNull**|3|指出提供者傳回型別為 VT_Null 的 VARIANT 值，而且欄位不是空的。|  
|**adFieldOK**|0|預設值。 表示已成功新增或刪除此欄位。|  
|**adFieldOutOfSpace**|22|指出提供者無法取得足夠的儲存空間來完成移動或複製作業。|  
|**adFieldPendingChange**|0x40000|表示欄位已刪除，然後重新加入（也許是使用不同的資料類型），或先前具有 **adFieldOK** 狀態的欄位值已變更。 欄位的最終格式將會在呼叫[Update](../../../ado/reference/ado-api/update-method.md)方法之後修改[Fields](../../../ado/reference/ado-api/fields-collection-ado.md)集合。|  
|**adFieldPendingDelete**|0x20000|指出 **刪除** 作業導致狀態設定。 呼叫**Update**方法之後，欄位已標記為要從**Fields**集合中刪除。|  
|**adFieldPendingInsert**|0x10000|指出 **附加** 作業造成設定的狀態。 呼叫**Update**方法之後，**欄位**已標示為要加入**Fields**集合中。|  
|**adFieldPendingUnknown**|0x80000|指出提供者無法判斷哪些作業造成欄位狀態的設定。|  
|**adFieldPendingUnknownDelete**|0x100000|指出提供者無法判斷哪些作業會導致設定欄位狀態，而且在呼叫**Update**方法之後，欄位將會從**Fields**集合中刪除。|  
|**adFieldPermissionDenied**|9|表示欄位無法修改，因為它定義為唯讀。|  
|**adFieldReadOnly**|24|表示資料來源中的欄位定義為唯讀。|  
|**adFieldResourceExists**|19|指出提供者無法執行作業，因為物件已經存在於目的地 URL，而且無法覆寫物件。|  
|**adFieldResourceLocked**|18|指出提供者無法執行作業，因為有一或多個其他應用程式或進程鎖定了資料來源。|  
|**adFieldResourceOutOfScope**|25|指出來源或目的地 URL 超出目前記錄的範圍。|  
|**adFieldSchemaViolation**|11|指出此值違反了欄位的資料來源架構條件約束。|  
|**adFieldSignMismatch**|5|表示提供者所傳回的資料值已簽署，但 ADO 域值的資料類型未簽署。|  
|**adFieldTruncated**|4|指出從資料來源讀取時，已截斷可變長度的資料。|  
|**adFieldUnavailable**|8|指出從資料來源讀取時，提供者無法判斷值。 例如，資料列是剛建立的，資料行的預設值無法使用，而且尚未指定新值。|  
|**adFieldVolumeNotFound**|21|指出提供者找不到 URL 所指出的儲存磁片區。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 這些常數沒有 ADO/WFC 對等專案。  
  
## <a name="applies-to"></a>套用至  
 [Status 屬性 (ADO Field)](../../../ado/reference/ado-api/status-property-ado-field.md)
