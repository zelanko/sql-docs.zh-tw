---
description: 欄位相關的錯誤資訊
title: 欄位相關的錯誤資訊 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: af7aee82f8568cafcc35ac0e78d13386822888fb
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991259"
---
# <a name="field-related-error-information"></a>欄位相關的錯誤資訊
如果錯誤與欄位直接相關-例如，如果資料遺失或欄位的類型不正確，您可以藉由檢查 **field** 物件的 **Status** 屬性來取得有關此問題原因的詳細資訊。 這個屬性已增強，可提供問題的相關特定資訊。 因此，例如，當調用**調用失敗時**，可以藉由檢查每個受影響記錄中**欄位**的**Status**屬性來判斷問題的原因。 屬性將包含 **FieldStatusEnum** 常數中的其中一個值。 下表包含錯誤發生時，特定的相關值。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adFieldCantConvertValue**|2|表示無法在不遺失資料的情況下抓取或儲存欄位。|  
|**adFieldDataOverflow**|6|指出從提供者傳回的資料會使欄位的資料類型溢位。|  
|**adFieldDefault**|13|指出設定資料時，會使用欄位的預設值。|  
|**adFieldIgnore**|15|指出當設定來源中的資料值時，已略過此欄位。 提供者未設定任何值。|  
|**adFieldIntegrityViolation**|10|表示欄位無法修改，因為它是計算或衍生的實體。|  
|**adFieldIsNull**|3|表示提供者傳回 null 值。|  
|**adFieldOutOfSpace**|22|指出提供者無法取得足夠的儲存空間來完成移動或複製作業。|
