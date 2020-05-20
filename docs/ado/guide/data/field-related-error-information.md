---
title: 欄位相關的錯誤資訊 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- field-related errors [ADO]
- errors [ADO], field-related
ms.assetid: 5e7b1af4-996b-47c5-9161-c5575ad4fec9
author: rothja
ms.author: jroth
ms.openlocfilehash: e61850ca788f6cff11d2a665000f68b89cd3ed45
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82758286"
---
# <a name="field-related-error-information"></a>欄位相關的錯誤資訊
如果錯誤與欄位直接相關-例如，如果資料遺失或欄位的類型錯誤，您可以藉由檢查**欄位**物件的**Status**屬性來取得有關問題原因的詳細資訊。 這個屬性已經過增強，可提供問題的特定資訊。 因此，例如，當呼叫**UpdateBatch**失敗時，您可以檢查每個受影響記錄中**欄位**的**Status**屬性來判斷問題的原因。 屬性會包含**FieldStatusEnum**常數中的其中一個值。 下表包含錯誤發生時特別需要注意的值。  
  
|持續性|值|說明|  
|--------------|-----------|-----------------|  
|**adFieldCantConvertValue**|2|表示無法抓取或儲存欄位，而不會遺失資料。|  
|**adFieldDataOverflow**|6|表示從提供者傳回的資料溢位欄位的資料類型。|  
|**adFieldDefault**|13|表示設定資料時，使用欄位的預設值。|  
|**adFieldIgnore**|15|表示在設定來源中的資料值時，略過此欄位。 提供者未設定任何值。|  
|**adFieldIntegrityViolation**|10|表示欄位無法修改，因為它是計算或衍生的實體。|  
|**adFieldIsNull**|3|指出提供者傳回 null 值。|  
|**adFieldOutOfSpace**|22|指出提供者無法取得足夠的儲存空間來完成移動或複製操作。|
