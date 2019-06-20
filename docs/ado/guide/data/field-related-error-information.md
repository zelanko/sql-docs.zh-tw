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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: e18698d7fba50ce6a63938df574408367b8b20cf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66702019"
---
# <a name="field-related-error-information"></a>欄位相關的錯誤資訊
如果錯誤直接與相關欄位-比方說，如果資料遺失，或者它是錯誤的類型，欄位-您可以擷取問題的原因的詳細資訊藉由檢查**欄位**物件的**狀態**屬性。 這個屬性已經過增強，以提供特定問題的相關資訊。 因此，例如，當呼叫**UpdateBatch**失敗，問題的原因可以檢查來判斷**狀態**屬性**欄位**中每個受影響的功能記錄。 這個屬性會包含在值的其中一個**FieldStatusEnum**常數。 下表包含發生錯誤時，會特別感興趣的那些值。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adFieldCantConvertValue**|2|表示欄位無法擷取或儲存而不會遺失資料。|  
|**adFieldDataOverflow**|6|指出提供者傳回的資料造成溢位 欄位的資料類型。|  
|**adFieldDefault**|13|表示欄位的預設值已設定資料時使用。|  
|**adFieldIgnore**|15|表示這個欄位已略過，當設定資料來源中的值。 提供者未不設定任何值。|  
|**adFieldIntegrityViolation**|10|表示無法修改欄位，因為它是導出或衍生的實體。|  
|**adFieldIsNull**|3|表示提供者傳回 null 值。|  
|**adFieldOutOfSpace**|22|表示提供者無法取得足夠的儲存空間可完成的移動或複製作業。|
